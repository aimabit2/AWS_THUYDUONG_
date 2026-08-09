---
title: "Test the Interface Endpoint"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.4.3 </b> "
---

#### Workshop insight

This module validates that the on-premises client can reach the S3 Data Lake through the Interface endpoint and VPN. It demonstrates the hybrid connectivity path end-to-end.

#### What was verified

- the on-premises EC2 instance established a secure Session Manager shell,
- a test file was created and uploaded to the same S3 bucket using the private interface endpoint,
- the object appeared in the Data Lake without traversing public internet routes.

#### Why this matters

This validation proves the hybrid ingestion scenario for external financial data providers. It confirms that the secure data pipeline can accept input from outside AWS while preserving the same private network model.
