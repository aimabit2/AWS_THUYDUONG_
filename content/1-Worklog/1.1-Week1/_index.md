---
title: "Week 1 - Foundations of AWS Cloud Architecture, AI-Driven SDLC, and IAM Security"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Overview:

This week, I focused on three main themes: AWS infrastructure foundations, modern software development practices with GenAI/SDLC, and basic security knowledge through AWS Identity and Access Management (IAM).

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | AWS Global Infrastructure Foundations | Highly available systems should be designed with fault isolation, ideally across at least two Availability Zones (AZs). |
| B | Advanced GenAI and Modern Software Development Lifecycle (SDLC) | Software development with AI is more reliable when prompts are built on clear structure, include checkpoints, and are automatically tested. |
| C | Identity and Access Management (IAM) | Least privilege and using temporary IAM Roles are the safest choices for managing AWS permissions. |
---
### Domain A: AWS Global Infrastructure Foundations

Study the physical and logical boundaries in cloud infrastructure architecture to support the design of highly available systems.

#### *Monday, 22/06 | Cloud Computing Concepts and Benefits*

- Learn that cloud computing is a model delivering IT resources on demand over the Internet with pay-as-you-go pricing.
- Identify four core benefits of cloud computing:
  - cost optimization
  - faster development through automation and AI
  - flexibility in scaling and resource deployment
  - global deployment capability
- References: https://cloudjourney.awsstudygroup.com/1-introduce/

#### *Tuesday, 23/06 | AWS Infrastructure Topology Analysis*

- Study the components of AWS infrastructure including:
  - **Data Centers**
  - **Availability Zones (AZs)**
  - **Regions**
  - **Edge Locations**
- Learn that each Availability Zone is fault-isolated but connected via high-speed private networking.
- Understand that each Region contains at least three Availability Zones, while Edge Locations act as Points of Presence (PoP) for services like CloudFront CDN, AWS WAF, and Route 53.
- References:

> **Key takeaway:** A real production deployment should be designed across at least two Availability Zones to ensure fault isolation and service continuity.
---
### Domain B: Advanced GenAI and Modern Software Development Lifecycle

#### *Wednesday, 24/06 | Agentic AI and the Kiro IDE Framework*

- Learn the evolution of the software development lifecycle (SDLC), from AI assisting code generation to executing end-to-end feature development.
- Study how Kiro IDE/CLI converts a prompt into:
  - Requirements documentation
  - System architecture
  - Timeline checkpointing to create safe restore points and support rollback when needed
- References:

#### *Thursday, 25/06 | Advanced Context Management and Property-Based Testing (PBT)*

- Analyze Advanced Context Management through the Model Context Protocol (MCP) to connect multiple data sources such as:
  - documentation
  - databases
  - APIs
  - UI design
- Learn Property-Based Testing (PBT), a method that automatically generates many randomized test datasets from requirements described in EARS, instead of writing each test case manually.
- References:

> **Key takeaway:** Effective AI-enabled software development requires clear specifications, full context management, and automated testing mechanisms to ensure product quality.
---
### Domain C: Identity and Access Management (AWS IAM)

#### *Friday, 26/06 | Authentication and Authorization Structure*

- Learn the core components of AWS IAM, including: **Root User, IAM Users, Groups, JSON Policies**, and **IAM Roles**.
- Learn that the **Root User** should be protected with **Multi-Factor Authentication (MFA)** and avoided for daily activities.
- Understand the role of each IAM component:
  - **IAM Users** provide long-term credentials for people.
  - **Groups** support managing users by role-based access control (Role-Based Access Control - RBAC).
  - **Policies** define the permissions that users or services are allowed.
  - **IAM Roles** provide temporary credentials for AWS services or other resources to access each other securely.
- References:

> **Key takeaway:** Apply the **Least Privilege** principle and prioritize IAM Roles with temporary credentials when AWS services need to access one another.

#### *Saturday, 27/06 | Knowledge Consolidation and Review*

- Summarize the technical notes of Week 1 and systematize the main concepts about AWS architecture, Agentic AI, and AWS IAM.
- Review the learned concepts to strengthen understanding and prepare for the next weeks.
- References:
---
### Results Achieved

- Built a structured knowledge base on AWS core infrastructure, AI-driven SDLC (Kiro IDE), and IAM security mechanisms.
- Understood how to design fault-tolerant systems using AWS **Availability Zones** and **Regions**.
- Mastered the role of **Model Context Protocol (MCP), Property-Based Testing (PBT)**, and **Timeline Checkpointing** in elevating AI-assisted software quality.
- Understood and applied AWS IAM security principles, especially **Least Privilege**, **MFA** for Root User, and preferred **IAM Roles** for service-to-service access.
- Completed a solid foundation in AWS Cloud and modern software development methods, serving as a basis for learning and implementing Data Engineering projects in the weeks ahead.
