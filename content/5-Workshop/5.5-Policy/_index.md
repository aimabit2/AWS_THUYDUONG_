---
title: "VPC Endpoint Policies"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

#### Workshop narrative

This section explains why endpoint policies are essential for a secure financial data lake. An endpoint policy narrows access permissions for traffic traversing a VPC endpoint.

#### Key point

Even when S3 traffic is private, it may still be too broad if every bucket is reachable. A VPC endpoint policy allows the platform to limit access to only approved financial buckets.

#### Example policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowSpecificS3Bucket",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::your-bucket-name",
        "arn:aws:s3:::your-bucket-name/*"
      ]
    }
  ]
}
```

#### Why this matters

In a financial analytics platform, the least-privilege principle is vital. Endpoint policies prevent VPC resources from accessing unrelated S3 buckets, even if the traffic stays inside AWS.
