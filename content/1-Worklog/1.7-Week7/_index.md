---
title: "Week 7 - Cloud Security, Observability, and Threat Protection"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---
<!-- {{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}} -->


### Week 7 Overview

During Week 7, I focused on implementing comprehensive monitoring, threat detection, secret management, and edge security for the Financial Data Lake project. The week began with setting up centralized logging, performance metrics, and automated alarm systems using Amazon CloudWatch. Next, I enabled audit logging with AWS CloudTrail and configured automated threat detection through AWS GuardDuty. Finally, I secured sensitive credentials using AWS Secrets Manager and deployed AWS WAF rules to protect application endpoints from common web exploits.

| Domain | Main Focus | Key Takeaway |
| --- | --- | --- |
| A | System Observability & Monitoring with CloudWatch | Centralizing logs and metrics enables real-time operational visibility and proactive incident detection across cloud infrastructure.
| B | Audit Logging & Threat Detection with CloudTrail & GuardDuty | Audit Logging & Threat Detection with CloudTrail & GuardDuty
| C | Audit Logging & Threat Detection with CloudTrail & GuardDuty | Centralizing sensitive credentials and filtering malicious web traffic safeguards data integrity and prevents unauthorized access.

### Domain A: SYSTEM OBSERVABILITY & MONITORING WITH CLOUDWATCH

#### *Mon, Aug 03 | Configuring Centralized Logging & Custom Dashboards*

- Configured CloudWatch Log Groups and Log Streams to capture application and infrastructure logs across services.

- Created custom CloudWatch metrics to monitor data ingestion throughput, API error rates, and system latency.

- Built interactive CloudWatch Dashboards to visualize real-time Data Lake health, system performance, and active operational metrics.
- Ref:

> Key takeaway: Aggregating log streams and setting up custom dashboards streamlines system debugging and accelerates operational troubleshooting.

#### *Tue, Aug 04 | Setting Up Alarms & Automated Incident Notifications*

- Configured CloudWatch Alarms to trigger upon exceeding thresholds for API request errors, pipeline execution failures, and unusual latency spikes.

- Integrated CloudWatch Alarms with Amazon SNS to route real-time failure alerts directly to designated communication channels.

- Optimized metric evaluation periods to eliminate false-positive alert noise while maintaining rapid response capabilities.
- Ref:

> Key takeaway: Automated threshold alerting minimizes mean time to detection (MTTD) and ensures operational teams are notified immediately during failure events.

### Domain B: AUDIT LOGGING & THREAT DETECTION WITH CLOUDTRAIL & GUARDDUTY

#### *Wed, Aug 05 | Enabling Multi-Region Audit Logging with AWS CloudTrail*

- Enabled AWS CloudTrail across all regions to record API calls, management events, and data plane activities.

- Configured CloudTrail log file integrity validation and directed log storage to an encrypted, access-restricted S3 bucket.

- Integrated CloudTrail events with CloudWatch Logs to trigger alarms on critical security operations, such as IAM permission alterations or unauthorized S3 access attempts.
- Ref:

> Key takeaway: Immutable trail logs provide an auditable history of all AWS API activities, which is critical for compliance and forensic investigations.

#### *Thu, Aug 06 | Threat Detection & Vulnerability Scanning with AWS GuardDuty*

- Enabled AWS GuardDuty for continuous threat detection across AWS accounts and S3 bucket activity.

- Reviewed and categorized GuardDuty findings related to anomalous API calls, potential credential compromise, and unexpected data access patterns.

- Configured EventBridge rules to automatically route high-severity GuardDuty security findings to alert workflows.
- Ref:

> Key takeaway: Intelligent threat detection helps identify suspicious account activity early, enabling proactive security mitigation before data breaches occur.
### Domain C: SECRET MANAGEMENT & EDGE PROTECTION WITH SECRETS MANAGER & WAF

#### *Fri, Aug 07 | Centralizing Credentials & Edge Security Rules*

- Migrated hardcoded API keys, database credentials, and provider tokens to AWS Secrets Manager with automatic KMS encryption.

- Configured automatic secret rotation policies and updated Lambda and application execution roles with secure secret retrieve access.

- Deployed AWS WAF (Web Application Firewall) and attached Web ACLs to CloudFront distributions and API Gateway endpoints.

- Implemented WAF managed rule groups, SQL injection protection, cross-site scripting (XSS) filters, and rate-limiting rules to mitigate DDoS attacks.
- Ref:

> Key takeaway: Removing hardcoded credentials via Secrets Manager combined with edge filtering using WAF establishes robust defense-in-depth security.

### Achievements

- Implemented centralized logging, custom dashboards, and automated threshold alerts using Amazon CloudWatch.

- Established multi-region audit logging with CloudTrail and integrated log integrity validation for security compliance.

- Configured AWS GuardDuty for continuous threat monitoring and automated alert routing for high-severity findings.

- Centralized sensitive credentials using AWS Secrets Manager with automated KMS encryption and rotation rules.

- Secured frontend and API endpoints by deploying AWS WAF with managed security rules and rate-limiting protections.