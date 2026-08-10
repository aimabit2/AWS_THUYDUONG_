---
title: "Week 2 - AWS Storage, Compute, Networking, and Data Engineering Foundations"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---


### Week 2 Overview:

This week, I focused on AWS core services for storage, compute, and networking, while also beginning the team Data Engineering project.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | AWS Storage and Compute Foundations | Amazon S3 and Amazon EC2 are core services for building scalable data storage and flexible compute resources. |
| B | AWS Networking and Hybrid Connectivity | A well-designed VPC with layered security is the foundation for secure hybrid systems. |
| C | Data Engineering Project Kickoff | Defining a clear ETL architecture and local ingestion pipeline lays the groundwork for future cloud deployment. |

### Domain A: AWS Storage and Compute Foundations

#### *Monday, 29/06 | Amazon S3, Data Lake, and Data Warehouse*
- Studied **Amazon S3** as AWS’s highly scalable object storage service.
- Distinguished the roles of **Amazon S3**, **Data Lake**, and **Data Warehouse** in modern data architectures.
- Learned bucket and object concepts, data organization, metadata, access control mechanisms, and common enterprise use cases such as backup, big data analytics, and Data Lake implementation.
- Compared structured analytical storage (**Data Warehouse**) with raw data repositories (**Data Lake**) to understand each model’s role in the Data Engineering workflow.
- References:
> **Key takeaway:** Amazon S3 is the primary storage platform for building scalable Data Lakes, while Data Warehouses focus on analytical performance over processed data.

#### *Tuesday, 30/06 | Amazon EC2 and Static Website Hosting*
- Studied basic Amazon EC2 concepts, including:
  - EC2 instance types
  - key pairs
  - security groups
  - application deployment workflows
- Learned how to provision and manage virtual servers on AWS.
- Practiced hosting a static website with Amazon S3 to understand how to store and distribute a website without a dedicated web server.
- References:
> Key takeaway: Amazon EC2 provides flexible compute capacity, while Amazon S3 is a cost-effective and highly available solution for hosting static websites.

### Domain B: AWS Networking and Hybrid Connectivity

#### *Wednesday, 01/07 | Amazon VPC and AWS Site-to-Site VPN*
- Studied **Amazon Virtual Private Cloud (VPC)**, including:
  - CIDR planning
  - Regions
  - Availability Zones
  - Subnets
  - Route Tables
  - Internet Gateway (IGW)
  - Security Groups
  - Network ACLs
- Researched subnet segmentation strategies for:
  - Public subnets
  - Private subnets
  - VPN-only subnets
- Practiced establishing secure connectivity between on-premises systems and AWS Cloud through **AWS Site-to-Site VPN**.
- References:
> **Key takeaway:** A well-designed VPC combined with layered security and secure hybrid connectivity provides a strong foundation for highly available, secure cloud systems.

### Domain C: Data Engineering Project Kickoff

#### *Thursday, 02/07 | Project Planning and Pipeline Architecture*
- Officially started the team’s **Data Engineering** project.
- Participated in discussions to analyze business goals, system architecture, and implementation roadmap.
- Designed the overall ETL workflow covering:
  - **Data Ingestion**
  - **Bronze (Raw JSON)**
  - **Silver (Clean Parquet)**
  - **Gold (Feature Engineering)**
  - **Data Validation**
  - **Analytics**
- Reviewed project structure, development responsibilities, and cloud deployment strategy for future phases.
- References:

#### *Friday, 03/07 | Local Data Ingestion with VNStock3*
- Configured the local development environment by installing **VNStock3** and **Pandas**.
- Built the first Python script to collect Vietnamese stock market data using VNStock3.
- Successfully executed the initial ETL pipeline locally by storing raw data in the Bronze layer before continuing with cleaning, validation, and feature engineering.
- Reviewed the pipeline architecture and discussed future AWS deployment plans.
- References:
> **Key takeaway:** Separating the pipeline into Bronze, Silver, and Gold layers improves data quality, maintainability, and scalability while preparing the system for cloud-native deployment.

### Achievements
- Developed a strong understanding of AWS core services, including Amazon S3, Amazon EC2, Amazon VPC, and AWS Site-to-Site VPN.
- Gained practical experience designing secure cloud networking and hybrid connectivity architectures following AWS best practices.
- Officially kicked off the team’s Data Engineering project and implemented the first local ETL pipeline stage using VNStock3.
- Built the technical foundation for future AWS deployment by combining cloud infrastructure knowledge with practical data engineering workflows.
