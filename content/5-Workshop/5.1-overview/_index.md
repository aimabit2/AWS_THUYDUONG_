---
title: "Overview & System Architecture"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---
### 5.1 Overview & System Architecture
#### 5.1.1. Context and Business Problem
The Vietnamese stock market, with over 1,600 non-financial listed companies across three exchanges (HOSE, HNX, and UPCOM), presents a major challenge in monitoring and evaluating corporate financial health. Financial statement data from data providers is often fragmented, asynchronous in metric naming, and inconsistent in format.

The system is designed to fully automate the end-to-end pipeline: from raw data scraping, ETL standardization, Data Lake storage, and financial ratio matrix calculation, to financial distress risk labeling using Vietnamese regulatory rules combined with the Altman Z-Score. This dataset is then utilized to train Machine Learning models that provide early warning alerts for investors 1 to 2 years in advance.

#### 5.1.2. Summary Table of the 5-Tier AWS Serverless Architecture

| Architecture Layer | Key AWS Services | Key AWS Services | Estimated Cost/Month |
| :--- | :--- | :--- | :--- |
| **1. Ingestion Layer**  | EventBridge, Step Functions, AWS Lambda  | Quarterly/Annual cron scheduling, orchestrating parallel vnstock data scraping via Lambda, handling retry mechanisms on errors  | ~$0.30 USD   |
| **2. Data Lake & Storage Layer**  | Amazon S3 (Raw/Curated)  | Centralized storage of raw data (JSON/CSV) and standardized, labeled data (Apache Parquet)  | ~$0.30 USD  |
| **3. AI/ML Layer**  | AWS Glue ETL, Data Catalog, Amazon Athena  | Running Glue PySpark Jobs for schema standardization, Winsorization, ratio matrix & Z-Score calculation, catalog crawlers, and Athena SQL queries  | ~$0.85 USD  |
| **4. REST API & Security Layer**  | Amazon Cognito, API Gateway, AWS WAF, Lambda API  | JWT identity management, REST API routing, web attack prevention (DDoS, SQLi), and backend logic execution | ~$0.35 USD  |
| **5. Presentation & Alert**  | AWS Amplify, Amazon SES  | Hosting Web Dashboard (React/Next.js) and automatically sending risk warning emails to investors  | ~$0.40 USD  |


![Sơ đồ Kiến trúc Hệ thống 5 tầng trên AWS Cloud.](/images/diagram-3layer_v1.0.drawio.png)

- The diagram illustrates the data flow between Cloud services under the Serverless architecture. On the left, stock data sources flow through the Ingestion layer (EventBridge, Step Functions, Lambda) into the S3 Raw Bucket. Next, the data pipeline passes through the Processing layer (AWS Glue Jobs, Data Catalog) into the S3 Curated Bucket and connects to Athena. The REST API & Security layer (Cognito, API Gateway, WAF, Lambda Backend) acts as an intermediary for routing query requests. On the right, the Presentation & Notification layer renders the analytics UI on AWS Amplify and dispatches automated emails via Amazon SES.