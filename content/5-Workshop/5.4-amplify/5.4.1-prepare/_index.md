---
title: "Prepare the environment"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.4.1 </b> "
---

#### Workshop insight

This module sets up the hybrid on-premises simulation infrastructure required for private S3 access. It prepares the network, DNS, and routing components that support the on-premises workflow.

#### What was deployed

- a Route 53 Private Hosted Zone for S3 endpoint resolution,
- inbound and outbound Route 53 Resolver endpoints,
- VPN route table updates to route traffic from the on-premises VPC to the cloud.

#### Why this matters

Hybrid financial data ingestion needs reliable DNS and routing. This preparation ensures that the on-premises client can resolve private S3 endpoints and route traffic through the VPN without exposing sensitive data on the internet.
