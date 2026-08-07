---
title: "Week 1 - Foundations of AWS Cloud Architecture, AI-Driven SDLC, and IAM Security"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
<!-- {{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}} -->


### Week 1 Overview

This week covered three themes: AWS infrastructure fundamentals, modern Gen-AI / SDLC practices, and IAM security basics.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | AWS Global Infrastructure & Foundations | Resilient systems should be designed with fault isolation in mind, ideally across at least two AZs. |
| B | Advanced Gen-AI & Modern SDLC | AI delivery becomes reliable when prompts are backed by structure, checkpoints, and automated testing. |
| C | Identity & Access Management (IAM) | Least privilege and temporary roles are the safest default for AWS permissions. |

### Domain A: AWS Global Infrastructure & Foundations

Understanding physical and logical boundaries of cloud architecture for HA design.

#### Mon, Jun 22 | Cloud Computing Definitions & Benefits

- Defined cloud computing as on-demand IT resources delivered via the Internet with pay-as-you-go pricing.
- Identified four core benefits: 
     - cost optimization
     - accelerated development through automation and AI
     - high flexibility
     - global scale
- Ref:

#### Tue, Jun 23 | Infrastructure Topology Breakdown

- Studied the infrastructure layers: Data Centers, Availability Zones (AZs), Regions, and Edge Locations.
- AZs are fault-isolated and connected via high-speed private links.
- Regions contain at least three AZs, while Edge Locations serve as Points of Presence for CloudFront CDN, WAF, and Route 53.
- Ref:

> Key takeaway: A resilient production environment should keep a minimum dual-AZ footprint to preserve fault isolation.

### Domain B: Advanced Gen-AI & Modern SDLC

#### Wed, Jun 24 | The Agentic AI Shift & Kiro IDE Framework

- Explored the evolution of SDLC from basic code generation to end-to-end AI-driven feature implementation.
- Reviewed how Kiro IDE/CLI transforms prompts into requirements, architecture, and Timeline Checkpointing for safe snapshots and rollback.
- Ref:

#### Thu, Jun 25 | Advanced Context Management & Property-Based Testing (PBT)

- Analyzed Advanced Context Management using Model Context Protocol (MCP) to connect docs, databases, APIs, and UI designs.
- Studied Property-Based Testing (PBT), which generates many randomized test cases from EARS-formatted requirements instead of writing tests manually.
- Ref:

> Key takeaway: Professional AI delivery depends on structured specs, connected context, and automated boundary testing.

### Domain C: Identity & Access Management (AWS IAM)

#### Fri, Jun 26 | Authentication & Authorization Structures

- Deconstructed core IAM components: Root User isolation, IAM Users, Groups, JSON Policies, and IAM Roles.
- Root User should be protected with MFA and avoided for daily usage.
- IAM Users provide long-term credentials, Groups support RBAC management, Policies define permissions, and Roles provide temporary service-to-service credentials.
- Ref:

> Key takeaway: Enforce the Principle of Least Privilege and prefer temporary roles for cross-service permissions.

#### Sat, Jun 27 | Knowledge Consolidation & Review

- Organized the Week 1 technical notes and synthesized the main architectural concepts.
- Ref:

### Achievements

- Compiled a comprehensive, structured technical knowledge base covering AWS core infrastructure, Agentic SDLC (Kiro IDE), and IAM security mechanics.
