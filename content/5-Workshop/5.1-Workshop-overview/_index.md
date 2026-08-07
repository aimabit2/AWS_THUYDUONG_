---
title: "Workshop Overview"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

#### Executive summary

This workshop translates the architecture and automation narrative from the Proposal into a tangible AWS networking story. It demonstrates how a financial data platform can protect S3 Data Lake access without exposing sensitive traffic to the public internet.

#### Key themes

- Secure data ingestion for the Vietnam Financial Distress Prediction System.
- Private connectivity for cloud-native workloads and on-premises data clients.
- Service segmentation using VPC endpoints and endpoint policies.
- Validation of private S3 access from EC2 and hybrid networks.

#### Why this matters

In a production-grade financial analytics platform, raw financial statements and normalized datasets must remain within trusted networks. This workshop shows how to keep the data path private from the first upload through downstream analytics.

#### Architecture

![Overview Diagram](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)

The workshop architecture includes:
- **VPC Cloud**: the AWS environment hosting secure ingestion and analytics workloads.
- **VPC On-Prem**: a simulated on-premises network connected over VPN.
- **Amazon S3**: a centralized Data Lake for raw and curated financial data.
- **VPC Endpoints**: Gateway and Interface endpoints that keep S3 traffic private.
