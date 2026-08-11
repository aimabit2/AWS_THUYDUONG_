---
title: "Data Processing & Data Lake (AWS Glue ETL & Athena)"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### 5.3 DATA PROCESSING & DATA LAKE (AWS GLUE ETL & ATHENA QUERY)
#### 5.3.1. Data Processing Pipeline and Data Lake Optimization

Build and execute the ETL Process & Query Layer to transform raw data (Raw JSON) into a standardized financial indicator dataset (Curated Parquet Dataset), serving high-speed SQL queries and providing input data for Machine Learning models.

#### 5.3.2. Comparison Table of Data Lake Storage Format Efficiency


| Comparison Criteria  | Raw Format (JSON/CSV)   | Optimized Format (Snappy Parquet)   | Efficiency Improvement  |
| :--- | :--- | :--- | :--- |
| **S3 Storage Size** | 100% (Original) | ~20% (Snappy Compressed) | 80% reduction in S3 costs |
| **Data Structure** | Unpartitioned | Partitioned by year & quarter | Optimized data reading |
| **Athena Scan Volume** | Scans entire files | Scans only required columns & partitions| Accelerated SQL queries & reduced cost |
| **ETL Execution State** | Full re-processing | Remembers state with Job Bookmarks | Prevents duplication, saves DPUs |

#### 5.3.3. Step-by-Step Implementation Guide
- **Step 1: Create Amazon S3 Curated Bucket**
    1. Navigate to Amazon S3 ➔ Create bucket.
    2. Bucket name: `s3-vietnam-financial-curated-data-prod.`
    3. Select Region: `ap-southeast-1.`
    4. Create storage path: `curated/parquet/financial_features/.`

- **Step 2: Write AWS Glue ETL Job (PySpark / Python)**
The PySpark code on AWS Glue performs metric standardization, Winsorization noise handling, and Altman Z-Score computation:


```python
import sys
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from pyspark.sql.functions import col, when, expr, log

sc = SparkContext()
glueContext = GlueContext(sc)
spark = glueContext.spark_session

RAW_PATH = "s3://s3-vietnam-financial-raw-data-prod/raw/yearly/*.json"
OUTPUT_PATH = "s3://s3-vietnam-financial-curated-data-prod/curated/parquet/financial_features/"

# 1. Đọc dữ liệu JSON thô từ S3 Raw Bucket
df_raw = spark.read.option("multiline", "true").json(RAW_PATH)

# 2. Xử lý chuẩn hóa tên chỉ tiêu và tính chỉ số tài chính (Features)
df_features = df_raw.select(
    col("symbol"),
    col("year"),
    # Current Ratio (CR) = Current Assets / Current Liabilities
    (col("current_assets") / col("short_term_debt")).alias("CR"),
    # ROA = Net Profit / Total Assets
    (col("net_profit") / col("total_assets")).alias("ROA"),
    # ROE = Net Profit / Equity
    (col("net_profit") / col("equity")).alias("ROE"),
    # DAR = Total Debt / Total Assets
    (col("total_debt") / col("total_assets")).alias("DAR"),
    # WCTA = Working Capital / Total Assets
    ((col("current_assets") - col("short_term_debt")) / col("total_assets")).alias("WCTA"),
    # EBIT_TA = EBIT / Total Assets
    (col("ebit") / col("total_assets")).alias("EBIT_TA"),
    # MC_Debt = Market Cap / Total Debt
    (col("market_cap") / col("total_debt")).alias("MC_Debt")
)

# 3. Tính toán điểm số Altman Z-Score (Emerging Market Variant)
# Z = 6.56*WCTA + 3.26*ROA + 6.72*EBIT_TA + 1.05*MC_Debt
df_zscore = df_features.withColumn(
    "Z_Score",
    (6.56 * col("WCTA")) + (3.26 * col("ROA")) + (6.72 * col("EBIT_TA")) + (1.05 * col("MC_Debt"))
).withColumn(
    "distress_zone",
    when(col("Z_Score") <= 1.23, "Distress Zone (High Risk)")
    .when((col("Z_Score") > 1.23) & (col("Z_Score") <= 2.9), "Grey Zone (Medium Risk)")
    .otherwise("Safe Zone (Low Risk)")
)

# 4. Ghi kết quả dạng Parquet phân trang theo Năm vào S3 Curated Bucket
df_zscore.write \
    .mode("overwrite") \
    .partitionBy("year") \
    .parquet(OUTPUT_PATH)

print("Hoàn tất Glue Job xử lý dữ liệu và ghi Parquet!")
```
![Luồng điều phối Step Functions](/images/StepFunction.png)

- *Actual AWS Step Functions State Machine interface automatically invoking the AWS Glue Job task (StartJobRun), checking completion status (GetJobRun), and triggering the Glue Crawler scan.*

- **Step 3: Create AWS Glue Crawler & Data Catalog**
    1. Go to AWS Glue Console ➔ select Crawlers ➔ Click Add crawler.
    2. Crawler name: `crawler-vietnam-financial-curated.`
    3. Specify S3 data source: `s3://s3-vietnam-financial-curated-data-prod/curated/parquet/.`
    4. Create new Glue Database: `vietnam_financial_db.`
    5. Run Crawler. Once scanned, the table `financial_features` will automatically appear in the AWS Glue Data Catalog.

- **Step 4: Query Serverless SQL on Amazon Athena**
Open Amazon Athena, select the *vietnam_financial_db* database, and run a query to list enterprises with a high bankruptcy risk Z-Score:

```python
SELECT 
    symbol, 
    year, 
    round(z_score, 2) AS z_score, 
    distress_zone, 
    round(roa * 100, 2) AS roa_percent, 
    round(dar, 2) AS debt_ratio
FROM vietnam_financial_db.financial_features
WHERE z_score <= 1.23
ORDER BY year DESC, z_score ASC;
```