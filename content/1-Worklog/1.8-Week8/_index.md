---
title: "Week 8 - Building a Serverless Data Pipeline and Deploying a CloudFront-Optimized Frontend"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---



### Week 8 Overview

During Week 8, I focused on building an end-to-end serverless data processing pipeline and hosting a secure, optimized web frontend for the Financial Data Lake project. The week began with designing serverless backend APIs using AWS Lambda, API Gateway, and EventBridge for asynchronous event routing. Next, I established scalable data storage and analytical querying capabilities using Amazon S3 and Amazon Athena with partitioned dataset optimizations. Finally, I deployed and distributed the frontend application using AWS Amplify and Amazon CloudFront, implementing edge caching and secure content delivery.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | Serverless Backend & Event-Driven Architecture with Lambda, API Gateway & EventBridge | Decoupling backend services with event-driven triggers ensures high scalability, low latency, and resilient asynchronous data processing.
| B | Data Lake Storage & Serverless Analytics with S3 & Athena | Partitioning S3 data stores and optimizing Athena SQL queries significantly reduces query latency and operational analytics costs.
| C | Frontend Deployment & Edge Acceleration with Amplify & CloudFront | Hosting web assets with Amplify and routing traffic through CloudFront global edge networks improves application performance and security.

### Domain A: SERVERLESS BACKEND & EVENT-DRIVEN ARCHITECTURE WITH LAMBDA, API GATEWAY & EVENTBRIDGE

#### *Mon, Aug 10 | Designing RESTful APIs with API Gateway & AWS Lambda*

- Designed and deployed RESTful API endpoints using Amazon API Gateway to expose financial data processing features.

- Developed stateless AWS Lambda functions in Python/Node.js to handle business logic, data validation, and request transformation.

- Implemented CORS configuration, request validation schemas, and custom API Gateway authorizers for secure client access.
- Ref:

> Key takeaway: Combining API Gateway with Lambda creates a highly available, auto-scaling backend API layer without the overhead of server management.

#### *Tue, Aug 11 | Asynchronous Workflow Integration with Amazon EventBridge*

- Configured custom EventBridge Event Busses to decouple system microservices and handle asynchronous event publishing.

- Created EventBridge Rules to route real-time financial transaction events directly to target Lambda execution functions.

- Implemented Dead-Letter Queues (DLQ) and retry policies for failed event execution handling to guarantee data processing reliability.
- Ref:

> Key takeaway: Event-driven architecture powered by EventBridge enables seamless service integration and improves system fault tolerance.

### Domain B: DATA LAKE STORAGE & SERVERLESS ANALYTICS WITH S3 & ATHENA

#### *Wed, DATA LAKE STORAGE & SERVERLESS ANALYTICS WITH S3 & ATHENA*

- Structured Amazon S3 storage buckets into distinct Bronze (raw), Silver (processed), and Gold (aggregated) data lake zones.

- Configured S3 Bucket Policies, KMS encryption at rest, and S3 Lifecycle Rules to transition aged logs and dataset archives to lower-cost storage tiers.

- Implemented S3 Event Notifications to automatically trigger downstream Lambda data parsing workflows upon file upload.
- Ref:

> Key takeaway: A well-structured multi-tier S3 layout paired with automated lifecycle rules optimizes both security compliance and storage expenditure.

#### *Thu, Aug 13 | Interactive Serverless Data Analytics with Amazon Athena*

- Set up Glue Data Catalog tables and metadata schemas pointing to partitioned Parquet files stored in Amazon S3.

- Executed optimized SQL analytical queries using Amazon Athena to extract ad-hoc financial metrics and reporting insights.

- Applied Parquet file conversion and dataset partitioning (by year/month/day) to dramatically decrease data scanned per query and cut execution costs. 
- Ref:

> Key takeaway: Leveraging columnar formats like Parquet with Athena partitioning delivers lightning-fast SQL queries at a fraction of traditional database costs.

### Domain C: FRONTEND DEPLOYMENT & EDGE ACCELERATION WITH AMPLIFY & CLOUDFRONT



#### *Fri,  Aug 14 | Web Application Deployment & CDN Acceleration with Amplify & CloudFront*

- Deployed the frontend web dashboard using AWS Amplify with automated CI/CD pipeline integration linked to the Git repository.

- Configured Amazon CloudFront distributions in front of S3 static hosting and API Gateway endpoints for global edge caching.

- Optimized CloudFront caching behaviors, Custom Response Headers, and SSL/TLS certificate integration via AWS Certificate Manager (ACM).
- Ref:

> Key takeaway: Combining AWS Amplify for CI/CD deployments with CloudFront CDN caching minimizes latency for global end-users while ensuring high web availability.

### Achievements

- Built a scalable serverless API layer using Amazon API Gateway and AWS Lambda with built-in validation and security authorization.

- Architected an event-driven integration workflow using Amazon EventBridge with dead-letter queue exception handling.

- Organized a multi-tier S3 Data Lake structure with automated event-driven processing and cost-efficient lifecycle rules.

- Enabled high-performance serverless analytics on S3 datasets using Amazon Athena and Parquet data partitioning.

- Streamlined frontend deployment with AWS Amplify CI/CD pipelines and accelerated global content delivery using Amazon CloudFront distributions.