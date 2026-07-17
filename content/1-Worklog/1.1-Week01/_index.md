---
title: "Week 1"
date: 2026-04-20
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

**Weekly objectives:**
- Design the cloud-native high-availability networking topology.
- Configure Amazon VPC with public and private subnets across multiple Availability Zones.
- Establish internet connectivity and secure routing for public-facing layers.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday | Created the core Amazon VPC with a custom CIDR block. | Apr 20 |
| Tuesday | Provisioned public and private subnets across multiple Availability Zones. | Apr 21 |
| Wednesday | Deployed the Internet Gateway and attached it to the VPC. | Apr 22 |
| Thursday | Configured Public Route Tables to route external traffic via the Internet Gateway. | Apr 23 |
| Friday | Set up NAT Gateways in public subnets to enable secure outbound internet for private subnets. | Apr 24 |

**Weekly results achieved:**
- **Monday:**
  - Result Achieved: VPC established successfully, isolating the application network.
  - Lesson: Proper network segmentation is critical for separating public web traffic from private data stores.
- **Tuesday:**
  - Result Achieved: Subnets allocated across AZs for high availability support.
  - Lesson: Distributing subnets ensures fault tolerance in case of single Availability Zone disruptions.
- **Wednesday:**
  - Result Achieved: Internet Gateway attached and functional.
  - Lesson: An Internet Gateway should only be mapped to public subnets to maintain private subnet isolation.
- **Thursday:**
  - Result Achieved: Public routing active and verified.
  - Lesson: Explicitly defining public route tables prevents accidental public exposure of internal resources.
- **Friday:**
  - Result Achieved: NAT Gateways deployed and routing verified from private zones.
  - Lesson: NAT Gateways allow private instances to download updates securely without accepting inbound external connections.
