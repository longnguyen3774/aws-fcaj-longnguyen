---
title: "Week 12"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

**Weekly objectives:**
- Orchestrate the end-to-end pipeline using Amazon EventBridge Scheduler.
- Implement global CloudWatch monitoring dashboards and failure alarms.
- Conduct comprehensive system testing and initiate resource cleanup optimization.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Configured Amazon EventBridge Scheduler rules to automate the daily ETL pipeline at off-peak hours. | Jul 06 |
| Tuesday | Linked EventBridge triggers to sequentially launch Glue jobs and the `ML-Forecast-Server` training run. | Jul 07 |
| Wednesday | Built a centralized Amazon CloudWatch Dashboard consolidating web, ETL, and ML status metrics. | Jul 08 |
| Thursday | Configured Amazon SNS notifications to alert teams via email on pipeline or API failures. | Jul 09 |
| Friday | Performed a final end-to-end live test run and cleaned up redundant staging resources. | Jul 10 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Automated daily calendar schedules successfully activated within EventBridge.
  - Lesson: Event-driven orchestration removes manual operational steps, ensuring forecasting models are always up to date.
- **Tuesday:**
  - Result Achieved: Orchestration sequence validated: Glue extraction triggers Spark engineering, followed by ML training.
  - Lesson: Chaining dependent tasks prevents model training scripts from running on missing or corrupted data snapshots.
- **Wednesday:**
  - Result Achieved: CloudWatch dashboard built, providing full visibility into system health and key metrics.
  - Lesson: Centralized monitoring dashboards simplify system tracking and speed up troubleshooting across cloud components.
- **Thursday:**
  - Result Achieved: SNS alert rules successfully active and tested for instant error reporting.
  - Lesson: Proactive alerting keeps engineering teams informed of pipeline processing issues before they impact business operations.
- **Friday:**
  - Result Achieved: System verified fully operational, with old staging files cleaned up to optimize monthly costs.
  - Lesson: Regularly cleaning up temporary cloud assets ensures long-term infrastructure remains highly cost-effective.
