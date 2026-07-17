---
title: "Week 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Weekly objectives:**
- Configure Amazon CloudFront CDN for global static asset distribution.
- Deploy the External Application Load Balancer to manage public traffic.
- Deploy the Internal Application Load Balancer to secure microservice communications.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Created the Amazon CloudFront distribution pointing to the external load balancer origin. | May 18 |
| Tuesday | Provisioned the public-facing External Application Load Balancer (ALB). | May 19 |
| Wednesday | Configured External ALB target groups and routing rules for the Web storefront. | May 20 |
| Thursday | Provisioned the private Internal Application Load Balancer. | May 21 |
| Friday (Office visit) | Linked Web instances to target the Internal ALB for API routing. | May 22 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: CloudFront distribution activated with default caching behaviors.
  - Lesson: Using a CDN significantly reduces load on web servers by caching static media assets closer to users.
- **Tuesday:**
  - Result Achieved: External ALB deployed into public subnets ready to receive internet requests.
  - Lesson: External ALBs bridge internet users to private compute resources securely.
- **Wednesday:**
  - Result Achieved: Target groups passing health checks on port 80/443.
  - Lesson: Configuring accurate health check paths prevents traffic from routing to unresponsive or broken instances.
- **Thursday:**
  - Result Achieved: Internal ALB active in private subnets, abstracting the API microservices.
  - Lesson: An internal load balancer prevents the frontend web app from needing direct instance IPs for API calls.
- **Friday (Office visit):**
  - Result Achieved: End-to-end routing from external traffic down to internal API confirmed.
  - Lesson: Dual-ALB architectures provide a solid isolation barrier between public tiers and sensitive business APIs.
