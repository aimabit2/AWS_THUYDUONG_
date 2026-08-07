---
title: "Test the Gateway Endpoint"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

#### Workshop insight

This module validates that the VPC Cloud environment can upload and access S3 objects through the Gateway endpoint. It demonstrates the end-to-end private connectivity for the S3 Data Lake.

#### What was verified

- an S3 bucket was created for workshop data.
- a test object was uploaded from an EC2 instance inside VPC Cloud.
- the object was listed and retrieved successfully without using an Internet Gateway.

#### Why this matters

The test proves that private data lake ingestion is real and operational. It confirms that cloud-native financial data ingestion can occur inside a secure AWS network without exposing sensitive payloads to the public internet.

#### Key takeaway

A successful Gateway endpoint validation means the S3 Data Lake can reliably support secure ETL workloads and analytics jobs in the VPC Cloud.
