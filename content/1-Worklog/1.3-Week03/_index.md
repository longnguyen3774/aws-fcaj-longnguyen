---
title: "Week 3"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

**Weekly objectives:**
- Initialize the central transaction and analytical database schemas.
- Provision staging S3 buckets for the data landing zone.
- Configure Amazon CloudWatch baseline alarms for infrastructure monitoring.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Designed the PostgreSQL database relational schemas for storefront transactions. | May 04 |
| Tuesday | Created the analytical schema for the feature tables in the training database. | May 05 |
| Wednesday | Provisioned the primary S3 bucket `fashion-retail-model-storage` and data landing zones. | May 06 |
| Thursday | Configured S3 bucket policies and server-side encryption (SSE-S3). | May 07 |
| Friday | Set up baseline CloudWatch billing and infrastructure alarms. | May 08 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Storefront transaction schemas finalized with foreign keys and indexes.
  - Lesson: Proper initial indexing on transaction tables accelerates subsequent Glue extraction queries.
- **Tuesday:**
  - Result Achieved: Feature store analytical schema optimized for time-series features.
  - Lesson: Analytical schemas should be structured to handle efficient reads for ML training datasets.
- **Wednesday:**
  - Result Achieved: S3 buckets deployed with structured prefixes (`/landing`, `/features`, `/models`).
  - Lesson: Organizing S3 prefixes early simplifies the access control and paths for ETL and ML training scripts.
- **Thursday:**
  - Result Achieved: Encryption and access blocks activated on all buckets.
  - Lesson: Enforcing Amazon S3 block public access ensures sensitive corporate data is never exposed publicly.
- **Friday:**
  - Result Achieved: Alarms configured to alert on budget thresholds and CPU utilization.
  - Lesson: Early monitoring setup prevents unexpected cost overruns during the infrastructure rollout phase.
