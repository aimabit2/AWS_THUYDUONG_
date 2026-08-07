---
title: "Access S3 from On-premises"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

#### Workshop narrative

This section extends the financial data platform beyond AWS by simulating private access from an on-premises network. It uses an S3 Interface endpoint and a VPN-connected hybrid architecture.

For a risk analytics system, some data sources may originate outside AWS. This module shows how to keep those flows private and integrated with the same S3 Data Lake used by cloud workloads.

#### What this section covers

- the hybrid connectivity model for an on-premises client,
- the role of PrivateLink Interface endpoints for on-premise S3 access,
- how DNS and VPN routing enable the hybrid path.

#### Key takeaway

An S3 Interface endpoint over a VPN lets on-premises systems access S3 securely while preserving the private network boundary of the data lake.

#### Related pages

- [Prepare the environment](4.1-prepare/)
- [Create interface endpoint](4.2-create-interface-enpoint/)
- [Test interface endpoint](4.3-test-endpoint/)
- [DNS simulation](4.4-dns-simulation/)
