---
title: "Week 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

**Weekly objectives:**
- Develop a serverless forecast serving layer using AWS Lambda.
- Expose the Lambda prediction function via Amazon API Gateway.
- Verify low-latency inference outputs from the endpoint.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Authored the AWS Lambda inference function handling real-time forecast requests. | Jun 29 |
| Tuesday | Packaged inference scripts with lightweight prediction dependencies into a Lambda deployment layer. | Jun 30 |
| Wednesday | Created an Amazon API Gateway HTTP API to serve as the public serverless endpoint entry. | Jul 01 |
| Thursday | Configured Lambda routing triggers and environment paths to fetch artifacts from S3 dynamically. | Jul 02 |
| Friday | Conducted endpoint latency and load testing using API testing tools. | Jul 03 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Lambda function written to load model artifacts from S3 and generate SKU demand predictions.
  - Lesson: Serverless inference removes the need to run expensive, idle prediction servers 24/7.
- **Tuesday:**
  - Result Achieved: Deployment package minimized to ensure fast Lambda cold-start speeds.
  - Lesson: Keeping Lambda deployment packages small directly minimizes latency spikes during cold starts.
- **Wednesday:**
  - Result Achieved: API Gateway endpoint live, offering secure and scalable URL access points.
  - Lesson: API Gateway scales automatically to match incoming storefront request spikes seamlessly.
- **Thursday:**
  - Result Achieved: Lambda function successfully reads model models from S3 and serves live predictions.
  - Lesson: Dynamic model loading allows teams to update production forecasts just by uploading new artifacts to S3.
- **Friday:**
  - Result Achieved: Endpoint latency remained under 150ms during simulated concurrent traffic testing.
  - Lesson: Low-latency inference ensures storefront users experience zero slowdowns during real-time lookups.
