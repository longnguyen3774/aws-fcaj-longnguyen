---
title: "Week 1"
date: 2026-05-15
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

# Work Log: Model Development with SageMaker, S3 Storage, and EC2 API Deployment

> **Week 1 - Friday, May 15, 2026:** Focused on building and training machine learning models using Amazon SageMaker, managing datasets and artifacts via Amazon S3, and deploying the trained model as a production-ready API on Amazon EC2.

---

### Objectives for the Day

- Configure an **Amazon SageMaker** notebook instance to build, train, and evaluate a machine learning model.
- Leverage **Amazon S3** as a secure, high-durability storage solution for raw datasets and trained model artifacts.
- Deploy the finalized model as a scalable **API endpoint on Amazon EC2** using a Python web framework (e.g., FastAPI/Flask).
- Establish resource access controls and networking to ensure seamless integration between SageMaker, S3, and EC2.

---

### Machine Learning Workflows with Amazon SageMaker

#### 1. Environment & Notebook Setup
- Provisioned a SageMaker Notebook Instance (`ml.t3.medium`) to serve as the centralized development environment.
- Configured IAM Execution Roles with specific permissions (`AmazonSageMakerFullAccess`) allowing SageMaker to read training data from and write model artifacts to Amazon S3.

#### 2. Model Building & Training Pipeline
- Developed a data preprocessing script to clean and format features before training.
- Utilized built-in algorithms/custom Docker containers within SageMaker to execute the training job.
- Monitored training metrics (loss, accuracy) directly through SageMaker Logs integrated with Amazon CloudWatch.
- Outputted the serialized model file (`model.tar.gz`) directly to a designated S3 bucket upon successful completion.

---

### Data & Artifact Lifecycle Management with Amazon S3

#### 1. Bucket Structure & Storage Tiers
To support the machine learning lifecycle, I structured an S3 bucket with organized prefixes for clear data separation:

| Folder / Prefix | Data Type | Storage Class | Description |
|---|---|---|---|
| `/raw-data/` | Original Datasets | S3 Standard | Low latency for frequent read access during data exploration. |
| `/processed-data/` | Preprocessed Features | S3 Standard | Cleaned data ready to be ingested by training jobs. |
| `/model-artifacts/` | `model.tar.gz` files | S3 Standard | Output directories containing trained model weights. |

#### 2. Durability & Security Controls
- Verified **99.999999999% (11 nines)** data durability guarantees provided by S3 to ensure critical model artifacts are never lost.
- Applied explicit **S3 Bucket Policies** restricting access solely to the SageMaker training role and the EC2 production instance.

---

### Model API Deployment on Amazon EC2

#### 1. EC2 Instance Provisioning
- Launched an Amazon EC2 instance (`t3.medium` or compute-optimized `c6i.large` depending on model size) running Amazon Linux 2023.
- Configured a **Security Group** allowing inbound traffic on standard web ports (`80`, `443`) and the custom API port (`8000`).

#### 2. API Implementation & Deployment Steps
- Cloned the deployment repository onto the EC2 instance containing a lightweight API framework (FastAPI/Flask).
- Configured a Python virtual environment and installed necessary dependencies (`boto3`, `torch`/`scikit-learn`, `uvicorn`).
- Wrote a script using `boto3` to pull the latest `model.tar.gz` file down from the Amazon S3 bucket during application startup.
- Set up a production-ready process manager (`systemd` or `pm2`) along with `Nginx` as a reverse proxy to host the prediction API endpoint.

---

### CLI Operations & Diagnostic Commands

When managing the infrastructure for training and deployment, these AWS CLI commands are used to check resource state and verify logs:

```bash
# 1. List active SageMaker notebook instances and their statuses
aws sagemaker list-notebook-instances   --query 'NotebookInstances[].{Name:NotebookInstanceName,Status:NotebookInstanceStatus,Type:InstanceType}'   --output table

# 2. Sync processed local data up to the S3 bucket
aws s3 sync ./processed-data/ s3://my-ml-model-bucket-2026/processed-data/

# 3. Check if the model artifact has been successfully uploaded to S3
aws s3 ls s3://my-ml-model-bucket-2026/model-artifacts/

# 4. Verify running EC2 instances hosting the production API
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"   --query 'Reservations[].Instances[].{ID:InstanceId,Type:InstanceType,IP:PublicIpAddress}'   --output table
```

---

### Study Schedule & Topics Completed

| Study Date | Core Topic Focus | Primary AWS Services Involved |
|---|---|---|
| **15/05/2026** | Model Development & Training | Amazon SageMaker, CloudWatch Logs |
| **15/05/2026** | Dataset & Model Weights Storage | Amazon S3, S3 Bucket Policies |
| **15/05/2026** | Production API Hosting & Deployment | Amazon EC2, VPC Security Groups |

---

### Week 1 Key Takeaways

1. **Decoupled Architecture:** Separating the compute layers (SageMaker for heavy training, EC2 for real-time inference) from the storage layer (S3) optimizes cost and performance.
2. **Seamless Permissions:** Properly configured IAM roles allow SageMaker and EC2 to securely communicate with S3 without hardcoding access keys inside application scripts.
3. **Artifact Portability:** Compiling model weights into a centralized `model.tar.gz` on S3 simplifies CI/CD workflows, allowing new production APIs on EC2 to effortlessly fetch updated models.

---

*Source: [First Cloud Journey - AWS Study Group](https://cloudjourney.awsstudygroup.com/)*
