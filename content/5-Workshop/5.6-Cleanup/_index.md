---
title: "Cleanup"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

#### Workshop conclusion

This cleanup section closes the loop on the workshop by describing the operational steps needed to remove temporary resources and preserve a clean AWS footprint.

#### What to clean

- S3 buckets used for workshop data.
- VPC endpoints provisioned for the lab.
- Route 53 Resolver rules and hosted zones created for the on-premises simulation.
- EC2 instances used for validation.
- VPC networking resources, route tables, and security groups created for the workshop.
- Any CloudFormation stacks or temporary infrastructure used for deployment.

#### Why this matters

Cleaning up is part of responsible AWS operations. It prevents unintended costs and ensures the workshop environment does not leave behind stale infrastructure.
