---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# AUTOMATED VIETNAMESE SECURITIES FINANCIAL DATA INGESTION AND ANALYTICS PLATFORM ON AWS SERVERLESS

#### Summary

This workshop is the practical extension of the Vietnam Financial Distress Prediction System proposal and the blog insights from our AWS Serverless implementation. It explains how a secure S3 Data Lake and private networking model are built and validated in a real-world financial analytics workflow.

The content focuses on the same core themes as Section 2 (Proposal) and Section 3 (Blogs Posted):
- automated and secure ingestion into Amazon S3,
- private access from AWS VPC and on-premises clients,
- endpoint-based access controls for sensitive financial data,
- and the operational validation of those patterns.

#### What you will review

- `5.1 Workshop overview`: the architectural design and business rationale.
- `5.2 Prerequisites`: the environment, permissions, and technical assumptions.
- `5.3 Access S3 from VPC`: the S3 Gateway endpoint use case for cloud-native ingestion.
- `5.4 Access S3 from On-premises`: the hybrid connectivity and PrivateLink extension.
- `5.5 VPC Endpoint Policies`: how to enforce least-privilege access to S3.
- `5.6 Cleanup`: the post-lab resource management and operational cleanup.
