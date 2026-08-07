---
title: "Create an S3 Interface endpoint"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.4.2 </b> "
---

#### Workshop insight

This module focuses on provisioning an S3 Interface endpoint for the hybrid environment. An Interface endpoint enables on-premises traffic to reach S3 over PrivateLink.

#### What was configured

- the `com.amazonaws.us-east-1.s3` interface endpoint was created in the cloud VPC,
- it was attached to private subnets with security group controls,
- DNS name management was prepared for the simulated on-premises network.

#### Why this matters

Interface endpoints are essential when the data source is external to AWS. They provide the same secure, private access model as the cloud-native Gateway endpoint but across a hybrid boundary.
