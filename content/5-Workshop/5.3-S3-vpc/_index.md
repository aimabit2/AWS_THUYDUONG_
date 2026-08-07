---
title: "Access S3 from VPC"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

#### Workshop narrative

This section connects the S3 Data Lake design from the Proposal to a concrete AWS networking pattern: a Gateway VPC endpoint for Amazon S3.

A Gateway endpoint enables VPC-hosted ETL workers, analytics services, and test instances to reach S3 without traversing the public internet. For a financial platform, this reduces exposure and ensures data ingestion remains inside AWS private networking.

#### What this section covers

- the role of Gateway endpoints in a secure data lake architecture,
- the operational benefit of keeping traffic on AWS internal infrastructure,
- how the VPC Cloud environment is configured to use S3 privately.

#### Key takeaway

A Gateway endpoint is the simplest and most effective way to connect VPC workloads to Amazon S3 securely when the resources are inside the same VPC.

#### Related pages

- [Create Gateway endpoint](3.1-create-gwe/)
- [Test Gateway endpoint](3.2-test-gwe/)
