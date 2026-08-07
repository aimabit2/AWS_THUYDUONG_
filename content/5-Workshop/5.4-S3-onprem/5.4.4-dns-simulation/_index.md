---
title: "DNS Simulation"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4.4 </b> "
---

#### Workshop insight

This module explains the DNS layer for hybrid S3 access. It shows how Route 53 forwarding rules and private hosted zones resolve the S3 interface endpoint from an on-premises network.

#### What was configured

- alias records for `s3.us-east-1.amazonaws.com` in a private hosted zone,
- a Route 53 Resolver forwarding rule from the on-premises VPC,
- verification that the on-premises instance resolved the endpoint to the private interface IPs.

#### Why this matters

DNS is a critical component of any PrivateLink architecture. This module demonstrates how the hybrid environment resolves the S3 endpoint consistently and privately, supporting data ingestion without external DNS exposure.
