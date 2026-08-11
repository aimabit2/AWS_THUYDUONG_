---
title: "Week 3 - AWS Data Lake Architecture and Financial Data Platform Design"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
--- 


### Week 3 Overview

During Week 3, I focused on understanding **AWS Data Lake architecture** and its supporting services through the AWS Building Data Lakes on AWS whitepaper. The knowledge gained was then applied to evaluate and improve the architecture, data ingestion strategy, and storage design of our **Financial Data Lake project.**

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | AWS Data Lake Foundations | Understanding the core architecture and design principles of AWS Data Lakes provides the foundation for building scalable, cost-effective, and analytics-ready data platforms.
| B | Data Ingestion, Storage & Governance | Organizing data into logical storage zones and applying proper ingestion, metadata, and governance strategies improve data quality, discoverability, and long-term maintainability.
| C | Financial Data Lake Architecture Enhancement | Applying AWS Data Lake best practices helps design a scalable ETL architecture that supports analytics, dashboard visualization, and future machine learning applications.
---
### Domain A: AWS DATA LAKE FOUNDATIONS

#### *Mon, Jul 06 | Building Data Lakes on AWS – Architecture Overview*

- Studied the concept of **Data Lakes** and their role in modern data-driven organizations. 
- Explored the AWS reference architecture for building scalable and secure Data Lakes. 
- Learned the differences **between traditional databases**, **Data Warehouses**, and **Data Lakes**in terms of storage, scalability, and analytical capabilities. 
- Reviewed the core AWS services used within a Data Lake architecture, including Amazon S3, AWS Glue, Amazon Athena, AWS Lambda, and AWS Lake Formation. 

- Ref:

> Key takeaway: Amazon S3 serves as the central storage layer of an AWS Data Lake, while compute and analytics services remain decoupled, enabling scalable and cost-efficient data processing.

#### *Tue, Jul 07 | Data Ingestion & Data Collection Strategies*

- Studied various data ingestion approaches, including batch ingestion, streaming ingestion, and incremental data loading. 
- Learned how AWS ingestion services integrate with **Amazon S3** for centralized storage. 
- Reviewed best practices for designing scalable ingestion pipelines with **AWS Lambda** and **Amazon EventBridge**. 
- Evaluated different ingestion strategies for collecting Vietnamese financial market data from multiple public data providers. 

- Ref:

> Key takeaway: **Batch-oriented ingestion** provides a simple, reliable, and cost-effective solution for financial datasets that are updated periodically rather than continuously.
---
### Domain B: DATA LAKE STORAGE & DATA PROCESSING

#### *Wed, Jul 08 | Organizing Data Lakes with Amazon S3*

- Explored best practices for organizing datasets within Amazon S3 using logical storage zones. 
- Learned the purposes of Raw, Curated, and Analytics (Feature) layers in a modern Data Lake architecture. 
- Studied partitioning strategies, metadata organization, naming conventions, and lifecycle management for efficient storage and querying. 
- Analyzed how proper storage organization improves downstream ETL performance and analytical efficiency. 

- Ref:

> Key takeaway: A well-designed storage hierarchy improves maintainability, query performance, and scalability while supporting future machine learning and analytics workloads.

#### *Thu, Jul 09 | Data Processing, Metadata Management & Governance*

- Studied **AWS Glue** for ETL processing, schema discovery, and metadata catalog management. 
- Learned how **AWS Glue** Crawlers automatically identify datasets and build centralized metadata repositories. 
- Explored **AWS Lake Formation** for secure data governance, access control, and permission management across multiple datasets. 
- Reviewed best practices for ensuring data quality, consistency, and governance throughout the Data Lake lifecycle. 

- Ref:

> Key takeaway: Metadata management and centralized governance are essential for maintaining discoverable, secure, and reusable datasets within enterprise-scale Data Lakes.
---
### Domain C: PROJECT ARCHITECTURE ENHANCEMENT

#### *Fri, Jul 10 | Applying AWS Data Lake Architecture to the Financial Data Platform*

- Applied AWS Data Lake architectural principles to evaluate and refine the team's Financial Data Lake project. 
- Reviewed the proposed ETL workflow, including Data Ingestion, Raw Zone, Curated Zone, Feature Store, Analytics, and Monitoring components. 
- Evaluated AWS service selection for the project, including Amazon S3, AWS Lambda, AWS Glue, Amazon Athena, CloudWatch, and Terraform. 
- Discussed architectural improvements related to scalability, maintainability, cost optimization, and future machine learning integration. 

- Ref:

> Key takeaway: Applying AWS architectural best practices early in the project establishes a scalable and maintainable foundation for future analytics, visualization, and AI-driven financial applications.
---
### Achievements

- Developed a comprehensive understanding of **AWS Data Lake** architecture and its supporting services. 
- Learned best practices for data ingestion, storage organization, metadata management, and governance within AWS. 
- Strengthened knowledge of scalable ETL workflows using **Amazon S3, AWS Lambda, AWS Glue, and Amazon Athena**. 
- Applied AWS architectural principles to improve the design of the **Financial Data Lake** project, establishing a robust foundation for future analytics, dashboard development, and machine learning integration.
