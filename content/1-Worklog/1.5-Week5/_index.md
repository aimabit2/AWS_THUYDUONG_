---
title: "Week 5 - Principles of AWS Networking"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---



### Week 5 Overview

During Week 5, I focused on deploying the user-facing interface and setting up serverless query capabilities for the Financial Data Lake project. The week began with setting up automated frontend deployment using AWS Amplify, followed by configuring global content distribution and caching via AWS CloudFront. Finally, I configured AWS Athena to execute ad-hoc SQL queries and analytics directly over raw and processed financial datasets stored in Amazon S3.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | Frontend Deployment with AWS Amplify | Automating hosting and CI/CD workflows accelerates feature delivery while providing a seamless hosting environment for web applications.
| B | Global Distribution & Edge Caching with AWS CloudFront | Utilizing a global CDN improves application loading speeds, enhances security, and reduces direct load on origin resources.
| C | Serverless Data Analytics with AWS Athena | Querying S3 data directly via SQL enables cost-effective, high-performance analytics without the overhead of managing database infrastructure.

### Domain A: Querying S3 data directly via SQL enables cost-effective, high-performance analytics without the overhead of managing database infrastructure.

#### *Mon, Jul 20 | Setting Up AWS Amplify & CI/CD Pipeline*

- Configured AWS Amplify to host the frontend dashboard for visualizing financial data and execution status.

- Connected the project repository to set up automated build and deployment pipelines triggered by commit updates.

- Configured environment variables, build settings, and deployment branch strategies for staging and production environments.

- Monitored initial deployment builds and optimized build scripts to reduce bundle size and deployment times.
- Ref:

> Key takeaway: Automated CI/CD integration with AWS Amplify drastically reduces deployment overhead and ensures rapid iteration of frontend interfaces.

#### *Tue, Jul 21 | Managing Domain & Custom Environment Configurations*

- Configured custom domain mapping and automatic SSL/TLS certificate provisioning through AWS Amplify.

- Configured routing rules, rewrites, and redirects for single-page application (SPA) navigation.

- Integrated API Gateway endpoints into the frontend configuration to allow seamless secure calls to backend services.
- Ref:

> Key takeaway: Automated SSL management and routing configurations simplify custom domain setup while keeping application communication secure.

### Domain B: GLOBAL DISTRIBUTION & EDGE CACHING WITH AWS CLOUDFRONT

#### *Wed, Jul 22 | CloudFront Distribution Setup & Origin Configuration*

- Created an AWS CloudFront distribution to cache static frontend assets and accelerate API response delivery.

- Configured CloudFront origins pointing to S3 buckets and custom API Gateway endpoints.

- Implemented Origin Access Control (OAC) to restrict direct S3 bucket access, forcing traffic through CloudFront for enhanced security.
- Ref:

> Key takeaway: Securing S3 origins with CloudFront OAC enforces single-point ingress security while lowering latency for global end users.

#### *Thu, Jul 23 | Optimizing Cache Behaviors & Invalidation Strategies*

- Defined custom cache behaviors based on path patterns for static assets versus dynamic API endpoints.

- Configured TTL (Time-To-Live) settings and cache key policies to optimize edge hit ratios.

- Executed and tested cache invalidations when updating static frontend resources.

- Evaluated performance improvements using CloudFront compression (Gzip/Brotli) and edge location routing.
- Ref:

> Key takeaway: Tailoring cache behaviors according to asset types prevents stale data issues while maximizing response speed for static resources.
### Domain C: SERVERLESS DATA ANALYTICS WITH AWS ATHENA

#### *Fri, SERVERLESS DATA ANALYTICS WITH AWS ATHENA*

- Integrated Glue Data Catalog tables with AWS Athena to query Bronze and Silver financial data buckets in S3.

- Executed ad-hoc SQL queries to validate ingestion consistency, schema drift, and data formatting across historical records.

- Configured output location, query result encryption, and workgroups to control query costs and access permissions.

- Tested partition projection and columnar formats (Parquet) to minimize scanned data volume and speed up query execution.
- Ref:

> Key takeaway: Combining Glue Catalog with Athena allows instant SQL analytics over S3 data lakes while optimizing costs through proper data partitioning.

### Achievements

- Successfully deployed the project frontend interface using AWS Amplify with automated CI/CD integration.

- Established global content distribution using AWS CloudFront, securing origins with Origin Access Control.

- Optimized static asset caching, response compression, and cache invalidation strategies across edge locations.

- Configured AWS Athena to perform serverless SQL queries directly over raw and processed S3 financial data.

- Reduced analytical query costs and latency by configuring Glue Data Catalog integration and S3 partition structures.