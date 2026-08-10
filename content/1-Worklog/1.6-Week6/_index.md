---
title: "Week 6 - Infrastructure Automation & Continuous Delivery with AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Week 6 Overview

During Week 6, I focused on automating infrastructure deployment and establishing continuous integration and continuous delivery (CI/CD) pipelines for the Financial Data Lake project. The week began with defining Infrastructure as Code (IaC) using Terraform and AWS CloudFormation templates. Next, I configured fine-grained access policies using AWS IAM and organized automated data storage layers in Amazon S3. Finally, I built fully automated deployment pipelines using AWS CodePipeline and AWS CodeBuild to streamline application updates and infrastructure provisioning.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | Infrastructure as Code (IaC) with Terraform & CloudFormation | Declaring cloud infrastructure using code ensures consistent, repeatable, and version-controlled deployments across environments.
| B | Access Control & Storage Management with IAM & Amazon S3 | Implementing strict IAM least-privilege policies alongside structured S3 storage tiers guarantees data security and efficient lifecycle management.
| C | Automated CI/CD Pipelines with AWS CodePipeline & CodeBuild | Automating build, test, and deployment workflows accelerates release cycles and eliminates manual configuration errors.

### Domain A: INFRASTRUCTURE AS CODE (IaC) WITH TERRAFORM & CLOUDFORMATION

#### *Mon, Jul 27 | Modularizing Infrastructure with Terraform & CloudFormation*

- Authored Terraform modules and AWS CloudFormation templates to provision cloud infrastructure resources programmatically.

- Defined state management strategies using S3 remote backends and DynamoDB state locking to enable safe team collaboration.

- Parametrized resource configurations to support seamless deployment across staging and production environments.

- Executed plan, validation, and dry-run tests to evaluate resource dependencies and prevent unintended drift.
- Ref:

> Key takeaway: Managing infrastructure via declarative code simplifies environmental reproducibility and enforces version control for cloud assets.

#### *Tue, Jul 28 | Provisioning Automated Staging & Production Environments*

- Deployed foundational networking, storage, and IAM roles using automated CloudFormation stack execution.

- Configured drift detection to identify and remediate manual configuration changes outside the IaC framework.

- Evaluated modular Terraform state management versus nested CloudFormation stacks for multi-tier architectures.
- Ref:

> Key takeaway: Automated environment provisioning eliminates configuration drift and ensures strict alignment between code definitions and live cloud resources.

### Domain B: ACCESS CONTROL & STORAGE MANAGEMENT WITH IAM & AMAZON S3

#### *Wed, Jul 29 | Implementing IAM Security Controls & Least-Privilege Policies*

- Designed granular IAM roles, policies, and service trust relationships for automated deployment tools and applications.

- Configured identity-based and resource-based policies to restrict unauthorized cross-service operations.

- Enforced least-privilege principles by scoping down permission boundaries for automated build agents and deployment roles.

- Ref:

> Key takeaway: Strict IAM access controls minimize the attack surface by ensuring services only hold the minimal permissions necessary for execution.

### Domain C: 

#### *Thu, Jul 30 | Structuring Amazon S3 Data Layers & Lifecycle Rules*

- Configured structured S3 bucket topologies for raw Bronze, curated Silver, and analytical Gold data layers.

- Implemented default server-side encryption (KMS/S3-managed), bucket policies, and public access blocks.

- Established S3 Lifecycle rules to automatically transition older datasets to Glacier cold storage for cost optimization.

- Enabled bucket versioning and object locking to prevent accidental data deletion or tampering.

- Ref:

> Key takeaway: Layered S3 storage combined with automated lifecycle policies optimizes data governance and storage costs over extended periods.

### Domain C: AUTOMATED CI/CD PIPELINES WITH AWS CODEPIPELINE & CODEBUILD

#### *Fri, Jul 31 | Building Continuous Integration & Deployment Workflows*

- Configured AWS CodePipeline to automate multi-stage workflows spanning source control, build, test, and deployment stages.

- Created custom buildspec.yml files for AWS CodeBuild to automate unit testing, linting, and infrastructure deployment scripts.

- Integrated automated gate checks, approval stages, and rollback mechanisms upon pipeline failure.

- Connected S3 source triggers and repository Webhooks to initiate automated builds upon new code commits.
- Ref:

> Key takeaway: Integrating CodePipeline with CodeBuild creates an automated release mechanism that speeds up feature delivery while maintaining build quality.

### Achievements

- Defined modular Terraform and CloudFormation templates for automated provisioning of Data Lake infrastructure.

- Established secure S3 bucket topologies with encryption, versioning, and automated lifecycle storage policies.

- Implemented fine-grained IAM roles and least-privilege permission boundaries for build agents and cloud services.

- Constructed automated CI/CD pipelines using AWS CodePipeline and CodeBuild for seamless continuous delivery.

- Reduced manual operational overhead by fully automating build, test, and infrastructure deployment processes.