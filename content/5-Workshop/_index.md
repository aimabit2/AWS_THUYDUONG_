---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

 
# VIETNAM STOCKS FINANCIAL DATA COLLECTION & ANALYTICS WORKSHOP (AWS SERVERLESS)
### 5.1 Workshop Overview
#### 1. Overview

The Vietnam stock market (HOSE, HNX, UPCOM) contains over 1,600 non-financial listed companies whose financial statement data is often fragmented, inconsistent, and costly to process manually. This hands-on workshop provides a step-by-step guide to building and deploying an end-to-end Financial Distress Prediction System running on a five-tier AWS Serverless architecture.

The system automates the workflow from raw data scraping, ETL normalization, Data Lake storage, financial ratio calculation, regulatory and Altman Z-Score labeling, to ML model training, Web dashboard visualization, and real-time investor alerts.

- **Target audience**: Data Engineers, Cloud Architects, Financial Analysts, MLOps Engineers, and students/researchers in IT/Finance.
- **Estimated operating cost**: ~$1.50 – $3.00 USD/month using a cost-optimized Serverless pay-as-you-go approach.

#### 2. Workshop Objectives

After completing this workshop, participants will be able to:

- **Automate the ingestion pipeline** using Amazon EventBridge, AWS Step Functions, and AWS Lambda/ECS to extract financial data from vnstock.
- **Build a Serverless Data Lake and ETL** with AWS Glue PySpark Jobs to normalize schemas, exclude financial-sector companies, perform Winsorization (1%-99%), convert to Snappy-compressed Parquet, and query with Amazon Athena.
- **Deploy AI/ML pipelines and a Feature Store** using Amazon SageMaker Feature Store, Studio, and serverless endpoints to train and serve models (e.g., XGBoost, Random Forest, LightGBM).
- **Implement secure APIs and auth** with Amazon Cognito, API Gateway, and AWS WAF.
- **Visualize and alert** via a Web Dashboard on AWS Amplify and automated email notifications through Amazon SES when a company enters a high-risk zone.
- **Manage cost and cleanup** using Infrastructure as Code (IaC) and documented resource cleanup procedures to avoid unexpected charges.

#### Workshop modules

| Module | Lab title | Summary |
| :--- | :--- | :--- |
| **5.1** | **Overview & System Architecture** | Problem overview, objectives, five-tier AWS Serverless architecture, and deployment checklist. |
| **5.2** | **Automated Data Ingestion Pipeline** | Create S3 Raw Buckets, implement Lambda crawlers for vnstock, filter non-financial tickers, orchestrate with EventBridge & Step Functions. |
| **5.3** | **Data Processing & Data Lake (AWS Glue ETL, Data Catalog & Athena)** | Create S3 Curated Buckets, author Glue PySpark Jobs for schema normalization, Winsorization, compute financial features & Altman Z-Score, run Crawlers and query with Athena. |
| **5.4** | **REST API & User Authentication (Cognito, API Gateway & Lambda API)** | Configure Cognito User Pools, secure API Gateway with WAF, and implement Lambda backend APIs. |
| **5.5** | **Web Dashboard & Email Alerts (Amplify, Lambda & SES)** | Deploy a React/Next.js dashboard on Amplify and configure SES-based alerting for high-risk companies. |
| **5.6** | **Resource Cleanup & Summary** | Step-by-step resource cleanup to avoid unexpected cloud charges and final project summary. |

1. [Overview & System Architecture](5.1-overview/)
2. [Automated Data Ingestion Pipeline](5.2-Pipeline/)
3. [Data Processing & Data Lake (AWS Glue ETL & Athena)](5.3-glue-config/)
4. [REST API & User Authentication (Cognito, API Gateway & Lambda API)](5.4-amplify/)
5. [Web Dashboard & Alerting (Amplify, Lambda & SES)](5.5-Policy/)
6. [Resource Cleanup & Summary](5.6-Cleanup/)
