---
title: "Week 2 - AWS Storage, Compute, Networking, and Data Engineering Foundations"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Week 2 Overview

This week focused on AWS storage and compute foundations, hybrid networking design, and the kickoff of the team Data Engineering project.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | AWS Storage & Compute Foundations | S3 and EC2 provide the basic building blocks for scalable data storage and flexible compute. |
| B | AWS Networking & Hybrid Connectivity | A well-planned VPC with layered security controls is the foundation of secure hybrid architectures. |
| C | Data Engineering Project Initiation | A clear ETL architecture and local ingestion pipeline create a strong base for cloud migration later. |

### Domain A: AWS Storage & Compute Foundations

#### Mon, Jun 29 | Amazon S3, Data Lake & Data Warehouse Fundamentals

- Explored Amazon S3 as AWS's scalable object storage service.
- Distinguished the roles of Amazon S3, Data Lakes, and Data Warehouses in modern data architectures.
- Learned bucket and object concepts, storage organization, metadata, access control mechanisms, and common enterprise use cases such as backup, big data analytics, and data lake implementation.
- Compared structured analytical storage (Data Warehouse) with raw data repositories (Data Lake) to understand their roles in a data engineering workflow.
- Ref:

> Key takeaway: Amazon S3 serves as the storage foundation for building scalable Data Lakes, while Data Warehouses focus on optimized analytical performance over processed datasets.

#### Tue, Jun 30 | Amazon EC2 Fundamentals & Static Website Hosting

- Studied Amazon EC2 fundamentals, including instance types, key pairs, security groups, and application deployment workflows.
- Learned how to provision compute resources and manage virtual servers within AWS.
- Practiced hosting a static website using Amazon S3 to understand cloud-native web hosting without dedicated web servers.
- Ref:

> Key takeaway: Amazon EC2 provides flexible compute capacity, while Amazon S3 enables highly available and cost-effective hosting for static web applications.

### Domain B: AWS Networking & Hybrid Connectivity

#### Wed, Jul 01 | Amazon VPC & AWS Site-to-Site VPN

- Studied Amazon Virtual Private Cloud (VPC), including CIDR planning, Regions, Availability Zones, Subnets, Route Tables, Internet Gateway (IGW), Security Groups, and Network ACLs.
- Learned subnet segmentation strategies such as Public, Private, and VPN-only subnets following AWS networking best practices.
- Practiced establishing secure hybrid connectivity between on-premises infrastructure and AWS Cloud using AWS Site-to-Site VPN.
- Ref:

> Key takeaway: A well-designed VPC architecture, combined with layered security controls and secure hybrid connectivity, forms the foundation of highly available cloud infrastructures.

### Domain C: Data Engineering Project Initiation

#### Thu, Jul 02 | Project Planning & Data Pipeline Architecture

- Officially started the team Data Engineering project.
- Participated in project discussions to analyze business objectives, system architecture, and implementation roadmap.
- Designed the overall ETL workflow consisting of Data Ingestion, Bronze (Raw JSON), Silver (Clean Parquet), Gold (Feature Engineering), Data Validation, and Analytics layers.
- Reviewed project structure, development responsibilities, and deployment strategy for future cloud migration.
- Ref:

#### Fri, Jul 03 | Local Data Ingestion with VNStock3

- Configured the local development environment by installing VNStock3 and Pandas.
- Developed the first Python-based data ingestion script to collect Vietnamese stock market data from VNStock3.
- Successfully executed the initial ETL pipeline locally by storing raw data in the Bronze layer before subsequent cleaning, validation, and feature engineering stages.
- Reviewed the pipeline architecture and discussed future deployment to AWS cloud services.
- Ref:

> Key takeaway: Separating the pipeline into Bronze, Silver, and Gold layers improves data quality, maintainability, and scalability while preparing the project for cloud-native deployment.

### Achievements

- Built a comprehensive understanding of AWS core services, including Amazon S3, Amazon EC2, Amazon VPC, and AWS Site-to-Site VPN.
- Acquired practical experience in designing secure cloud networking and hybrid connectivity architectures following AWS best practices.
- Successfully initiated the team's Data Engineering project by implementing the first stage of a local ETL pipeline using VNStock3.
- Established the technical foundation for future cloud deployment by combining AWS infrastructure knowledge with real-world data engineering practices.
