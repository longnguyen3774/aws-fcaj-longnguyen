---
title: "Week 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**Weekly objectives:**
- Deploy the full feature pipeline onto the managed AWS Glue Spark service.
- Configure target writing mechanisms from Glue back into the `training-db` RDS instance.
- Perform end-to-end data processing performance benchmarks.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Uploaded `glue_feature_engineering.py` to the AWS Glue scripts repository. | Jun 15 |
| Tuesday | Provisioned an AWS Glue Spark Job configuration allocating 2 Data Processing Units (DPUs). | Jun 16 |
| Wednesday | Integrated the PostgreSQL JDBC writer within the Spark script to push outputs to `training-db`. | Jun 17 |
| Thursday | Conducted a full scale test run of both sequential Glue ETL jobs. | Jun 18 |
| Friday | Profiled processing runtimes, memory metrics, and optimized Spark DPU resource allocations. | Jun 19 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Script versioned and stored securely in the deployment bucket.
  - Lesson: Maintaining explicit script versions protects the production data pipeline from accidental overwrites.
- **Tuesday:**
  - Result Achieved: Glue job initialized with minimal DPU capacity to minimize unnecessary costs.
  - Lesson: Starting with a small DPU count helps find the optimal balance between job execution speed and cloud costs.
- **Wednesday:**
  - Result Achieved: Spark output successfully written into the decoupled analytical feature tables.
  - Lesson: Writing outputs directly to a separate training database isolates model preparation loads from customer-facing storefronts.
- **Thursday:**
  - Result Achieved: Sequential execution completed, moving data from `fashion-rds` to S3, and finally to `training-db`.
  - Lesson: A cleanly decoupled ETL sequence forms a stable data supply chain for machine learning workflows.
- **Friday:**
  - Result Achieved: Pipeline tuned to finish in under 20 minutes, safely meeting operational budget goals.
  - Lesson: Profiling execution metrics ensures the cloud infrastructure operates efficiently as business data grows.
