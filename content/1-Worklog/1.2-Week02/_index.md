---
title: "Week 2"
date: 2026-05-22
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

# Work Log: High-Performance Distribution with CloudFront, Traffic Routing via ALB, and Dynamic Scalability with Auto Scaling

> **Week 2 - Friday, May 22, 2026:** Upgraded the single-instance API infrastructure from Day 1 into a highly available (High Availability) and auto-scaling architecture. Configured an Application Load Balancer (ALB), established an Auto Scaling Group for EC2 instances, and optimized global response latency using the AWS CloudFront content delivery network.

---

### Objectives for the Week

- Implement an **Application Load Balancer (ALB)** to distribute API incoming traffic evenly across backend virtual servers.
- Configure an **Auto Scaling Group (ASG)** coupled with Launch Templates to dynamically scale EC2 instances based on real-time application load.
- Deploy **AWS CloudFront (CDN)** as the outermost edge layer to reduce latency, optimize edge caching, and enhance overall API security.
- Perform operational failover testing and validate dynamic cloud resource scaling policies.

---

### Traffic Routing & Balancing with Application Load Balancer (ALB)

#### 1. Target Group and Health Check Configuration
- Provisioned an `Instance`-based Target Group routing traffic over HTTP on port `8000` (the dedicated API service port established on Day 1).
- Configured a precise **Health Check** policy targeting the `/health` endpoint of the API every 30 seconds, ensuring the ALB only routes active traffic to healthy, operational nodes.

#### 2. Load Balancer Deployment in VPC
- Launched an Internet-facing Application Load Balancer (ALB) stripped across multiple **Availability Zones (AZs)** to achieve maximum fault tolerance in the event of a datacenter outage.
- Restructured Security Groups for the ALB to exclusively listen to public inbound traffic on standard HTTP (`80`) and HTTPS (`443`) ports.

---

### Dynamic Elasticity with EC2 Auto Scaling

#### 1. Launch Template Configuration (Server Blueprint)
- Designed a standardized Launch Template incorporating configurations from the Day 1 machine: utilizing Amazon Linux 2023, instance type `t3.medium`, pre-packaged API code, and an IAM Execution Role with secure S3 read capabilities.
- Configured custom **User Data** execution scripts: when a new EC2 instance is launched, it automatically executes a `git pull` to fetch the latest API revision, downloads the most recent `model.tar.gz` archive from S3, and spins up the FastAPI daemon.

#### 2. Auto Scaling Group (ASG) & Scaling Policies
Established clear resource boundaries for the auto-scaling fleet to maintain operational efficiency:

| ASG Parameter | Target Capacity | Operational Metric & Purpose |
|---|---|---|
| **Desired Capacity** | 2 instances | The target baseline fleet size maintained during steady-state operations. |
| **Minimum Capacity** | 2 instances | The lower bound required to guarantee multi-AZ High Availability. |
| **Maximum Capacity** | 5 instances | The ceiling limit utilized to safeguard against runaway Operational Expenses (OpEx). |

- **Target Tracking Scaling Policy:** Activated automated tracking bound to the `Average CPU Utilization` metric. If the aggregate CPU utilization across the fleet passes a **70%** threshold, the ASG immediately provisions supplementary EC2 instances to distribute the compute load.

---

### Global Acceleration & Optimization with AWS CloudFront

#### 1. CloudFront Distribution Mapping
- Deployed a CloudFront Distribution acting as the public-facing gateway, mapping the external ALB endpoint as the **Origin Server** (Origin).
- Enforced strict redirect policies routing all standard HTTP web requests to encrypted HTTPS connections at the CloudFront Edge network layer.

#### 2. Cache Behavior Management
Implemented granular caching rules to balance execution speed against real-time data integrity requirements:

| API Path Pattern | Cache State | Technical Justification |
|---|---|---|
| `/static/*` or asset directories | Caching Enabled (Default 24h) | Offloads static heavy content to global Edge Locations close to users, drastically dropping backend EC2 request loads. |
| `/predict` (Model Inference API) | Caching Disabled (Bypass Cache) | Bypasses caching entirely to ensure every distinct inference request is routed directly to the backend EC2 fleet for real-time model evaluation. |

---

### Operational CLI & Diagnostic Commands

The following AWS CLI commands were executed to monitor target pool health, verify scaling metrics, and force edge synchronization:

```bash
# 1. Query the operational health status of backend EC2 instances inside the ALB Target Group
aws elbv2 describe-target-health \
  --target-group-arn arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-api-tg/abc123xyz

# 2. Inspect active capacity metrics and fleet membership for the Auto Scaling Group
aws autoscaling describe-auto-scaling-groups \
  --auto-scaling-group-names my-api-asg \
  --query 'AutoScalingGroups[].{Name:AutoScalingGroupName,Desired:DesiredCapacity,Instances:Instances[].InstanceId}'

# 3. Issue a manual cache invalidation across CloudFront to force update static assets
aws cloudfront create-invalidation \
  --distribution-id E1A2B3C4D5E6F7 \
  --paths "/static/*"

# 4. Audit recent scaling history and lifecycle behaviors of the ASG fleet
aws autoscaling describe-scaling-activities \
  --auto-scaling-group-name my-api-asg \
  --max-items 3

```

---

### Completed Core Topics & Schedule

| Study Date | Core Topic Focus | Primary AWS Services Involved |
| --- | --- | --- |
| **22/05/2026** | Network Traffic Routing & System Health Verification | Application Load Balancer (ALB) |
| **22/05/2026** | Automated Server Fleets Matched to Application Load | EC2 Auto Scaling Group, Launch Templates |
| **22/05/2026** | Global Content Delivery Network & Cache Optimization | AWS CloudFront (CDN) |

---

### Week 2 Key Takeaways

1. **Stateless Architecture Priority:** For Auto Scaling groups to execute successfully, application servers must remain entirely stateless. Offloading the heavy model assets (`model.tar.gz`) to S3 on Day 1 allowed newly spawned EC2 nodes to launch smoothly without local data binding errors.
2. **ALB & ASG Symbiosis:** This combination forms the backbone of infrastructure resilience. Manually terminating an EC2 instance proved that the ALB health checks quickly drop unhealthy nodes, while the ASG initiates a self-healing process to bring the fleet back up to capacity within minutes.
3. **Multi-Tiered Infrastructure Protection:** Positioning CloudFront upstream from the ALB accelerates international response times via the AWS global network backbone, while abstracting the origin load balancer IP to protect against directed DDoS attempts.

---

*Source: [First Cloud Journey - AWS Study Group*](https://cloudjourney.awsstudygroup.com/)