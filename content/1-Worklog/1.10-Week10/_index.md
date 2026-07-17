---
title: "Week 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Weekly objectives:**
- Deploy and configure the dedicated `ML-Forecast-Server` compute instance.
- Develop python machine learning model training scripts.
- Implement automated model artifact exports to Amazon S3.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Provisioned the `ML-Forecast-Server` using an Amazon EC2 t3.small instance. | Jun 22 |
| Tuesday | Installed Python modeling environments including Scikit-learn, XGBoost, and LightGBM. | Jun 23 |
| Wednesday | Authored the core training script to load historical feature matrices from `training-db`. | Jun 24 |
| Thursday | Implemented regression model training loops, cross-validation, and performance logging. | Jun 25 |
| Friday | Added serialization logic to export trained model artifacts (`.bin`/`.pkl`) directly to S3. | Jun 26 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Dedicated ML server instance active and restricted to secure network security groups.
  - Lesson: Using an isolated training server protects storefront web resources from CPU-heavy machine learning workflows.
- **Tuesday:**
  - Result Achieved: Data science dependencies configured and verified using pip virtual environments.
  - Lesson: Isolating package dependencies ensures consistent model execution across development and deployment environments.
- **Wednesday:**
  - Result Achieved: Successful feature ingestion verified from the analytical database into training dataframes.
  - Lesson: Direct database-to-dataframe loading minimizes disk usage overhead on the training server.
- **Thursday:**
  - Result Achieved: XGBoost and LightGBM regressors successfully trained, achieving accurate demand forecasting metrics.
  - Lesson: Comparing multiple algorithms ensures the best model variant is selected for production use.
- **Friday:**
  - Result Achieved: Trained model artifacts successfully exported to `fashion-retail-model-storage/models/`.
  - Lesson: Centralizing model artifacts in Amazon S3 creates a clear history of model versions for deployment management.
