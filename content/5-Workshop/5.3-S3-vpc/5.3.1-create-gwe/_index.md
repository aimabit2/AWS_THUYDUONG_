---
title: "Create a Gateway endpoint"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

#### Workshop insight

This module describes the creation of a Gateway VPC endpoint for Amazon S3 in the VPC Cloud environment. The endpoint behaves as a private route between VPC resources and S3, avoiding public internet egress.

#### Why it matters

In the Vietnam Financial Distress Prediction System, secure ingestion is paramount. A Gateway endpoint ensures that data landing in the S3 Data Lake can be produced and consumed by VPC-hosted workloads without leaving the AWS network.

#### What was configured

- an S3 Gateway endpoint was provisioned in the VPC Cloud.
- the endpoint was associated with the private route table used by the VPC Cloud subnets.
- the default endpoint policy was left in place while the private connectivity proof-of-concept was validated.

#### Practical benefit

This setup allows AWS Glue, Lambda, or EC2-based ingestion jobs to upload and download financial data securely, using AWS-native private routing instead of public internet paths.
