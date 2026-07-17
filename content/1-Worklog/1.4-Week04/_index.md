---
title: "Week 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Weekly objectives:**
- Launch the base EC2 instances for the storefront web application.
- Deploy the internal RESTful API microservice instances.
- Configure local application environments and database drivers.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Launched baseline Ubuntu EC2 instances within private subnets for the Web Front-end. | May 11 |
| Tuesday | Launched corresponding EC2 instances for the internal RESTful API tier. | May 12 |
| Wednesday | Installed dependencies, Node.js, and Python runtimes on both server types. | May 13 |
| Thursday | Configured PostgreSQL database client drivers and connection parameters. | May 14 |
| Friday (Office visit) | Conducted internal loopback and cross-tier connectivity tests. | May 15 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: Web storefront compute servers deployed into multiple availability zones.
  - Lesson: Placing compute instances in private subnets keeps them secure from direct external access.
- **Tuesday:**
  - Result Achieved: API servers successfully deployed into deep private subnets.
  - Lesson: API layers should remain completely isolated from the internet, relying on load balancers for access.
- **Wednesday:**
  - Result Achieved: Application runtimes and environment variables initialized.
  - Lesson: Standardizing the environment runtime setup across instances guarantees reliable application execution.
- **Thursday:**
  - Result Achieved: Database client configurations mapped safely using parameters.
  - Lesson: Hardcoding database credentials inside code must be avoided; config parameters should load dynamically.
- **Friday (Office visit):**
  - Result Achieved: Successful ping and telnet validation between web and API servers.
  - Lesson: Validating local tier routing confirms security groups are correctly permitting necessary inner-cluster traffic.
