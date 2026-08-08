---
title: "Automated Data Ingestion Pipeline"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Workshop context

This workshop assumes the same environment and goals described in the Proposal and Blogs Posted sections. It is not a generic AWS lab — it is specifically aligned to a secure financial data pipeline and risk analytics system.

#### Required environment

- An AWS account with permissions to manage VPC, EC2, S3, IAM, Route 53 Resolver, and CloudFormation.
- AWS CLI installed and configured.
- Familiarity with AWS networking concepts, especially VPC route tables, security groups, and VPC endpoints.
- Basic understanding of S3 Data Lake design and serverless ETL patterns.

#### Assumptions

- The reader already understands the serverless data pipeline architecture from Section 2.
- The security goal is to avoid public internet access for S3 traffic.
- The workshop is designed as a proof-of-concept for hybrid private data ingestion.

#### What this workshop proves

- private S3 access using Gateway endpoints for VPC compute,
- secure hybrid access using PrivateLink and VPN,
- policy-based access control for sensitive financial buckets.
