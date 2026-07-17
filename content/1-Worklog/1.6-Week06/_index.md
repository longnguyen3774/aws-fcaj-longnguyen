---
title: "Week 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Weekly objectives:**
- Deploy two parallel Amazon RDS PostgreSQL instances for transactional and analytical workloads.
- Configure secure DB Subnet Groups across multiple Availability Zones.
- Set up network security rules restricting database access to authorized web servers.
- Verify connectivity from private EC2 instances to the databases.

**Tasks to be deployed this week:**

| Day | Task | Date |
|---|---|---|
| Monday (Office visit) | Deployed the central transactional database `fashion-rds` using Amazon RDS PostgreSQL. | May 25 |
| Tuesday | Deployed the dedicated analytical database `training-db` using Amazon RDS PostgreSQL. | May 26 |
| Wednesday | Configured database Security Groups to restrict access, allowing inbound traffic only from the EC2 security group. | May 27 |
| Thursday | Set up DB Subnet Groups to distribute database instances across multiple private Availability Zones. | May 28 |
| Friday | Executed connection verification tests from private EC2 instances to both database endpoints. | May 29 |

**Weekly results achieved:**
- **Monday (Office visit):**
  - Result Achieved: RDS `fashion-rds` running on db.t3.micro (20 GiB storage) with automatic backups enabled.
  - Lesson: AWS RDS manages database provisioning and operating system patches, reducing administrative overhead.
- **Tuesday:**
  - Result Achieved: RDS `training-db` provisioned for storing processed training datasets.
  - Lesson: Decoupling live business databases from ML training stores isolates analytical query loads, protecting customer transaction performance.
- **Wednesday:**
  - Result Achieved: Configured firewall security group rules on port 5432, blocking all public IP addresses.
  - Lesson: Inbound database traffic should always be restricted to target application servers via security group IDs rather than static IPs.
- **Thursday:**
  - Result Achieved: Grouped subnets across different AZs, ensuring high availability database provisioning.
  - Lesson: Subnet groups allow RDS to maintain standby replicas in secondary zones for failover support.
- **Friday:**
  - Result Achieved: Connected to both databases using psql from inside the EC2 instance and initialized database tables.
  - Lesson: Validating connectivity from actual compute servers ensures routing tables and security groups are correctly aligned.
