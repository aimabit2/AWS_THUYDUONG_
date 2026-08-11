---
title: "Resource Cleanup & Summary"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

### 5.6 Resource Cleanup & Conclusion
To avoid incurring unintended AWS cloud service costs after completing the construction and testing of the workshop lab, our team provides the step-by-step resource cleanup process below.
#### 5.6.2. Resource Cleanup and Cost Avoidance Table

| Order  | AWS Service   | Required Cleanup Action | Required Cleanup Action |
| :--- | :--- | :--- | :--- |
| **1**| Amazon S3 | Empty & Delete `S3 Raw` and `S3 Curated Buckets` | Avoid static storage costs |
| **2** | AWS Glue | Delete Crawlers, ETL Jobs & Data Catalog Databases | Avoid Glue Schema Catalog fees |
| **3** | API Gateway & WAF | Delete REST APIs & gỡ bỏ Web ACLs trên WAF | Avoid API request and WAF hourly charges |
| **4** | Compute & Frontend | Delete Lambdas, Step Functions & Delete Amplify App | Avoid recurring compute and hosting charges |

#### 5.6.3. Step-by-Step Implementation Guide
1. **Delete AWS Amplify Application:**
    Access **AWS Amplify Console** ➔ select `app vietnam-financial-dashboard` ➔ Click **Actions** ➔ **Delete app**.
2. **Delete Amazon API Gateway & AWS WAF:**
    Go to **Amazon API Gateway** ➔ select `vietnam-financial-api` ➔ Click **Delete**.
    Go to **AWS WAF** ➔ delete the Web ACL attached to the API Gateway.

3. **Delete Amazon Cognito User Pool:**
    Go to **Amazon Cognito** ➔ select `vietnam-financial-user-pool` ➔ Delete App Client and click Delete user pool.
4. **Delete AWS Lambda Functions & Step Functions:**
    Go to **AWS Lambda Console** ➔ Delete functions: `lambda-ingestor-vnstock`, `lambda-backend-api`, `lambda-ses-alert`.
    Go to **AWS Step Functions** ➔ select data scraping State Machine ➔ Click **Delete**.

5. **Delete AWS Glue Jobs, Crawlers & Data Catalog:**
    Go to **AWS Glue Console** ➔ Delete Job `glue-job-pyspark-financial-etl`.
    Delete Crawler `crawler-vietnam-financial-curated`.
    Go to **Data Catalog Databases** ➔ Delete Database `vietnam_financial_db`.

6. **Delete Data and Amazon S3 Buckets**:
    Access **Amazon S3 Console**.
    Select `s3-vietnam-financial-raw-data-prod` ➔ Click **Empty** to purge all objects/versions ➔ Click **Delete**.
    Select `s3-vietnam-financial-curated-data-prod` ➔ Click **Empty** ➔ Click **Delete**.
---
### Workshop Summary
Upon completing the full lab series, you have mastered the process of building an end-to-end Financial Data Ingestion and Analysis System for Vietnamese Stocks on AWS Serverless 

    - Platform:Built an automated financial data scraping pipeline using Lambda, EventBridge, and Step Functions.
    - Cleaned and calculated financial ratio sets (CR ,  ROA ,  ROE ,  DAR ,  WCTA , Altman Z-Score) using PySpark on AWS Glue.
    - Queried high-speed partitioned Parquet data via SQL using Amazon Athena.
    - Secured APIs with Amazon Cognito, AWS WAF, and REST API Gateway.
    - Visualized data on an AWS Amplify Web Dashboard and dispatched bankruptcy risk warning emails via Amazon SES.
