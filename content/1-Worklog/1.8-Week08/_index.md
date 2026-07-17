---
title: "Week 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Weekly objectives:**
- Develop the PySpark feature engineering pipeline script.
- Implement distributed calculations for time-series features (lags, rolling averages).
- Optimize PySpark data transformations across large SKU partitions.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Initialized the `glue_feature_engineering.py` PySpark script structure. | Jun 08 |
| Tuesday | Implemented PySpark Window functions to compute 7-day and 14-day lagged sales features. | Jun 09 |
| Wednesday | Added distributed transformations for calculating 30-day rolling averages and sales velocity metrics. | Jun 10 |
| Thursday | Configured data partitioning columns based on SKU and store identifiers. | Jun 11 |
| Friday | Executed local Spark engine tests with small mock data samples. | Jun 12 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: PySpark environment configured with proper SparkSession initializations.
  - Lesson: PySpark handles massive scale time-series features efficiently compared to single-threaded database queries.
- **Tuesday:**
  - Result Achieved: Lag calculation functions verified across temporal data frames.
  - Lesson: Window partitioning by item and location ensures lags are calculated accurately without cross-contamination.
- **Wednesday:**
  - Result Achieved: Rolling averages and sales velocity features successfully appended to the feature matrix.
  - Lesson: Velocity metrics capture sudden market shifts, which improves the accuracy of demand forecasting models.
- **Thursday:**
  - Result Achieved: Data partitioned by SKU and store IDs to maximize distributed processing efficiency.
  - Lesson: Smart partitioning structures optimize resource usage across Spark clusters and accelerate query speeds.
- **Friday:**
  - Result Achieved: Mock pipeline run finished successfully with no runtime syntax errors.
  - Lesson: Pre-validating transformations on small sample batches saves significant debugging time and costs before running full AWS Glue jobs.
