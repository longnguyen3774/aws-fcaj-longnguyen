---
title: "Week 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Weekly objectives:**
- Establish the AWS Glue data catalog and connections.
- Develop the Python Shell ETL script for raw database extraction.
- Verify secure data transfer from RDS PostgreSQL into S3 landing zones.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Created AWS Glue Connection configurations for both `fashion-rds` and `training-db` databases. | Jun 01 |
| Tuesday | Developed the `de-fashion-rds-extract` script using the AWS Glue Python Shell environment. | Jun 02 |
| Wednesday | Configured S3 IAM data access permissions for the AWS Glue execution role. | Jun 03 |
| Thursday | Executed initial manual test runs of the Python extraction script. | Jun 04 |
| Friday | Validated the integrity and schema of extracted raw CSV files inside the S3 staging path. | Jun 05 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Glue catalog connections validated and successfully testing communication to RDS instances.
  - Lesson: Glue connections safely manage JDBC string credentials via VPC networking configurations.
- **Tuesday:**
  - Result Achieved: Python Shell script fully written to query daily storefront sales entries.
  - Lesson: Python Shell provides a lightweight, cost-effective runtime for pulling smaller daily transaction sets without Spark overhead.
- **Wednesday:**
  - Result Achieved: Glue service role authorized to write objects inside the target S3 landing prefixes.
  - Lesson: Strict IAM resource limits ensure the ETL process cannot read or write to unauthorized data store zones.
- **Thursday:**
  - Result Achieved: Data successfully pulled out of PostgreSQL tables and written to S3.
  - Lesson: Ensuring scripts handle exceptions properly prevents extraction jobs from failing silently during automated schedules.
- **Friday:**
  - Result Achieved: Raw transaction datasets verified in S3 with matching database row counts.
  - Lesson: Checking target file sizes and counts guarantees that the initial data ingestion step is completely reliable.
