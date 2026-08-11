---
title: "Automated Data Ingestion Pipeline"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---
### 5.2 Automated Data Ingestion Pipeline

#### 5.2.1. Initializing S3 Raw Bucket and Industry Filtering Rules

The first step in the ingestion pipeline is initializing the S3 Raw Bucket, which acts as a staging zone holding raw data in JSON/CSV formats. The system integrates an automated business filter to exclude ticker symbols belonging to 4 specific industry groups: Banking, Securities, Insurance, and Investment Funds, due to their distinct financial statement structures.

#### 5.2.2. Ingestion Stream Technical Specifications

| Component  | Technology / Parameter   | Detailed Execution Description   |
| :--- | :--- | :--- |
| **Script Runtime Environment** | AWS Lambda (Python 3.11+) | Runs script packaging the vnstock library to extract all 3 financial statements & stock prices |
| **Trigger Schedule** | Amazon EventBridge Cron | Configures automated cron jobs triggered at the end of each quarter/year |
| **Workflow Orchestrator** | AWS Step Functions State Machine | Orchestrates parallel execution, saves checkpoints, and handles exponential backoff retries on API errors|
| **Raw Storage Destination** | Amazon S3 Raw Bucket | Stores raw data structured as: *s3://financial-raw-data/ticker/year/quarter/* | 

#### 5.2.3. Step-by-Step Implementation Guide
- **Step 1: Initialize S3 Raw Bucket**
    1. Navigate to AWS Management Console ➔ select S3 service.
    2. Click Create bucket.
    3. Bucket name: `s3-vietnam-financial-raw-data-prod`.
    4. Select AWS Region: ap-southeast-1 (Singapore).
    5. Keep SSE-S3 (AES-256) default encryption and enable Bucket Versioning.
    6. Click Create bucket.

- **Step 2: Filter Non-Financial Enterprises List**
Because the Financial Statement structure of the banking and financial sector is fundamentally different from manufacturing/commercial enterprises, we filter out and exclude:
    - ❌ Banks
    - ❌ Securities Companies
    - ❌ Insurance Companies
    - ❌ Finance Companies & Investment Funds

✅ Retain only non-financial listed enterprises across 3 exchanges: HOSE, HNX, and UPCOM.

- **Step 3: Write AWS Lambda Ingestor Source Code with `vnstock`**


```python
import json
import boto3
import pandas as pd
from vnstock import financial_report

s3_client = boto3.client('s3')
BUCKET_NAME = 's3-vietnam-financial-raw-data-prod'

def lambda_handler(event, context):
    symbol = event.get('symbol', 'VNM')
    print(f"Bắt đầu cào dữ liệu cho mã: {symbol}")
    
    # 1. Cào Bảng cân đối kế toán
    balance_sheet = financial_report(symbol=symbol, report_type='BalanceSheet', frequency='Yearly')
    # 2. Cào Báo cáo Kết quả Kinh doanh
    income_statement = financial_report(symbol=symbol, report_type='IncomeStatement', frequency='Yearly')
    # 3. Cào Báo cáo Lưu chuyển Tiền tệ
    cash_flow = financial_report(symbol=symbol, report_type='CashFlow', frequency='Yearly')
    
    # Ghi dữ liệu thô vào S3 Raw Bucket
    raw_payload = {
        'symbol': symbol,
        'balance_sheet': balance_sheet.to_dict(orient='records'),
        'income_statement': income_statement.to_dict(orient='records'),
        'cash_flow': cash_flow.to_dict(orient='records')
    }
    
    s3_key = f"raw/yearly/{symbol}_financial_data.json"
    s3_client.put_object(
        Bucket=BUCKET_NAME,
        Key=s3_key,
        Body=json.dumps(raw_payload, ensure_ascii=False),
        ContentType='application/json'
    )
    
    return {
        'statusCode': 200,
        'body': f"Đã lưu thành công dữ liệu thô mã {symbol} vào S3: {s3_key}"
    }
```

- **Step 4: Initialize AWS Step Functions & EventBridge Orchestration Workflow**
    1. AWS Step Functions: Create a State Machine to iterate over the ticker list, invoke Lambda Ingestor in parallel, support retry mechanisms upon hitting rate limits, and automatically record log checkpoints.
    2. Amazon EventBridge Scheduler: Configure Cron Job rules to trigger Step Functions periodically (e.g., at 00:00 on the first day of every month) to automatically ingest the latest quarterly/yearly financial reports.

![Step Functions State Machine orchestration flow](/images/StepFunction.png)


*Description of Step Functions State Machine orchestration flow in the system:*

- **Start Workflow**: Automated triggers from Amazon EventBridge Cron Scheduler or manual invocation to activate the entire data pipeline.

- **Raw Data Ingestion & Storage Task**: Calls AWS Lambda / ECS Ingestor to scrape financial statements from `vnstock`, performs checkpointing, and saves JSON files to the `S3 Raw Bucket`.

- **AWS Glue ETL Job Task**: Step Functions transitions to invoke the **AWS Glue StartJobRun** task, automatically triggering PySpark ETL processes to clean raw data, calculate financial ratios *( CR ,  ROA ,  ROE ,  DAR ,  WCTA )*, and assign the **Altman Z-Score** insolvency risk label.

- **Catalog Update & Completion**: Upon successful completion of the Glue Job, Step Functions activates the AWS Glue Crawler to scan metadata and update the Glue Data Catalog. If errors occur, the system automatically triggers retry mechanisms and transitions to a warning Fail State.
