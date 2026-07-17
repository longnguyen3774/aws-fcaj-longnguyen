---
title: "Week 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Weekly objectives:**
- Implement AWS IAM least-privilege security policies and execution roles.
- Configure baseline Security Groups for multi-tier isolation.
- Set up VPC Flow Logs for network traffic auditing.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Defined IAM Least-Privilege Policies for EC2, Glue, and Lambda services. | Apr 27 |
| Tuesday | Created specific IAM Execution Roles and attached policy definitions. | Apr 28 |
| Wednesday | Configured baseline Security Groups for the Web, API, and DB layers. | Apr 29 |
| Thursday | Implemented Security Group nesting rules to restrict tier-to-tier traffic. | Apr 30 |
| Friday | Enabled VPC Flow Logs to log network traffic to Amazon CloudWatch. | May 01 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: IAM Policies drafted restricting actions to required resources only.
  - Lesson: Least-privilege access minimizes the blast radius of any potential credential compromises.
- **Tuesday:**
  - Result Achieved: Roles assigned to respective AWS services and validated.
  - Lesson: Using service roles removes the need for long-lived access keys inside instances or applications.
- **Wednesday:**
  - Result Achieved: Layered security groups initialized.
  - Lesson: Isolating web, application, and database tiers behind distinct security groups forms a strong defense-in-depth barrier.
- **Thursday:**
  - Result Achieved: Nested rules configured successfully (API only accepts Web traffic).
  - Lesson: Referencing Security Group IDs instead of static IP addresses ensures scaling groups maintain security bounds automatically.
- **Friday:**
  - Result Achieved: Flow logs active and streaming data to CloudWatch Logs.
  - Lesson: Continuous network logging is essential for security auditing, troubleshooting, and detecting anomalous behavior.
