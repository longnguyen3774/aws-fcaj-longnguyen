---
title: "Week 3"
date: 2026-05-25
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

# Work Log: Provisioning RDS Postgres Database, Automating ETL Workflows with AWS Glue, and Scheduling Serverless Cron Jobs via EventBridge

> **Week 3 - Monday, May 25, 2026:** Focused on building a structured data persistence layer using Amazon RDS PostgreSQL, designing an automated Extract, Transform, and Load (ETL) data pipeline via AWS Glue, and establishing time-based scheduling mechanisms using Amazon EventBridge.

---

### Objectives for the Week

- Provision and configure a secure, production-optimized **Amazon RDS PostgreSQL** relational database.
- Build an automated **ETL (Extract, Transform, Load)** pipeline with **AWS Glue** to crawl, clean, and ingest raw S3 datasets into the database.
- Automate pipeline execution schedules by designing serverless **Amazon EventBridge** rules.
- Validate data integrity post-transformation and implement secure, cross-service IAM permissions.

---

### Relational Database Management with Amazon RDS PostgreSQL

#### 1. Database Provisioning and Network Isolation
- Launched a stable **Amazon RDS PostgreSQL** instance, utilizing the `db.t3.micro` instance class within the AWS Free Tier boundaries for development testing.
- Created a dedicated **DB Subnet Group** spanning exclusively across the VPC’s Private Subnets, ensuring the database tier remains completely isolated from the public internet.
- Enabled **Auto Minor Version Upgrade** to let AWS automatically handle minor security patches for the PostgreSQL engine.

#### 2. Advanced Security Hardening
- Structured the **RDS Security Group** to strictly accept inbound traffic on the standard PostgreSQL port `5432` only when originating from the EC2 application fleet Security Group (from Day 2) or the AWS Glue network environment.
- Activated **Storage Encryption** at rest utilizing the default AWS Key Management Service (KMS) master key.

---

### Data Transformation Pipelines with AWS Glue

#### 1. Schema Discovery via Glue Crawler & Data Catalog
- Configured an **AWS Glue Crawler** targeted at the `/raw-data/` prefix within the designated Amazon S3 Bucket (created on Day 1).
- Executed the crawler to automatically analyze raw file structures (JSON/CSV) and map the extracted metadata schema into a logical table inside the central **AWS Glue Data Catalog**.

#### 2. Glue ETL Job Engineering (Python/Spark)
- Developed an isolated **AWS Glue ETL Job** using a Python/PySpark runtime environment to perform crucial data refining steps:
  - Dropped duplicate records and handled missing/null values systematically.
  - Normalized date-time formatting and cast machine learning feature columns into appropriate data types.
- Configured a JDBC (Java Database Connectivity) output block within the Glue Job to securely write the transformed, clean datasets directly into the target tables inside **RDS PostgreSQL**.

---

### Serverless Workflow Automation via Amazon EventBridge

#### 1. EventBridge Rule Configuration (Cron Scheduling)
- Transformed the manual ETL tasks into a fully automated pipeline by designing an **Amazon EventBridge Rule** running on a time-based schedule.
- Implemented a standard **Cron Expression** (`cron(0 1 * * ? *)`) to trigger the end-to-end data pipeline daily at 01:00 AM, taking advantage of low-peak operational hours.

#### 2. Target Mapping & Failure Handling
- Routed the EventBridge rule target directly to activate the newly created AWS Glue ETL Job.
- Configured an automated **Retry Policy** (up to 3 attempts) along with a Dead-Letter Queue (DLQ) mapped to an Amazon SQS queue to isolate failed invocation events for administrative debugging.

---

### Operational CLI & Diagnostic Commands

The following AWS CLI commands were utilized to audit the relational database deployment, trigger data crawlers, and monitor automated schedules:

```bash
# 1. Verify the operational status and connection endpoint of the RDS PostgreSQL instance
aws rds describe-db-instances \
  --db-instance-identifier my-postgres-db \
  --query 'DBInstances[].{Status:DBInstanceStatus,Endpoint:Endpoint.Address,Port:Endpoint.Port}'

# 2. Trigger an asynchronous AWS Glue Crawler execution to scan new files on S3
aws glue start-crawler --name my-s3-raw-data-crawler

# 3. Manually kick off the AWS Glue ETL Job and generate a runtime execution ID
aws glue start-job-run --job-name my-data-transform-job

# 4. Inspect the operational state and expression string of the EventBridge schedule rule
aws events describe-rule --name daily-etl-schedule-rule \
  --query '{Name:Name,State:State,Schedule:ScheduleExpression}'

```

---

### Completed Core Topics & Schedule

| Study Date | Core Topic Focus | Primary AWS Services Involved |
| --- | --- | --- |
| **25/05/2026** | Secure Relational Database Management & Isolation | Amazon RDS PostgreSQL, AWS KMS |
| **25/05/2026** | Metadata Discovery & Serverless ETL Orchestration | AWS Glue (Crawler, Data Catalog, Job) |
| **25/05/2026** | Serverless Cron Scheduling & Target Routing | Amazon EventBridge |

---

### Week 3 Key Takeaways

1. **Database Network Isolation Principle:** Relational databases should never be exposed directly to the public internet (`Publicly Accessible = No`). Restricting access strictly to internal Security Groups belonging to the EC2 application layer or the Glue ETL environment effectively minimizes the network attack surface.
2. **The Power of Centralized Metadata:** The AWS Glue Data Catalog serves as an essential central data dictionary. It allows indexing of vast data structures sitting on S3 without moving the actual data files, keeping subsequent analytical and ML workloads structured and highly organized.
3. **Transitioning to Serverless Event-Driven Architectures:** Replacing traditional, server-bound crontab setups with Amazon EventBridge eliminates the overhead costs of maintaining 24/7 idle host instances. The entire orchestration and compute layer (EventBridge + Glue) incurs costs exclusively during the exact seconds of code execution, drastically optimizing operational expenditures (OpEx).

---

*Source: [First Cloud Journey - AWS Study Group*](https://cloudjourney.awsstudygroup.com/)