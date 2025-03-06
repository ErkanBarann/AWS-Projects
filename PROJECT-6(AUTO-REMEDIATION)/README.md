# 🛠️ Auto-Remediation for ASG Desired Capacity

## 📌 Project Overview
TechPro-Soft uses a **'multiple environment to a single AWS account'** approach for EC2 deployments. The company has noticed frequent **outages** due to **junior engineers** mistakenly setting the **desired capacity** of the production **Auto Scaling Group (ASG) to 0**. 

Since **IAM permissions** are not modified for now, an **auto-remediation solution** is required to detect these changes and automatically restore the correct ASG configuration.

---

## 🚀 Solution Architecture

The proposed **auto-remediation system** consists of the following AWS services:

### 🔹 **EC2 Instances & ASG (Auto Scaling Group)**
- Contains production (`env: prd`) and development (`env: dev`) instances.
- ASG manages the lifecycle of EC2 instances.

### 🔹 **CloudWatch Alarms & Events**
- **Monitors ASG changes** and triggers an alert if desired capacity is set to `0`.
- Sends event notifications to trigger remediation workflows.

### 🔹 **AWS Lambda Function**
- Triggered when an ASG modification event is detected.
- Automatically resets the **desired capacity** to a predefined value.
- Logs remediation actions to **Amazon CloudWatch**.

### 🔹 **SNS Notifications**
- Sends alerts and updates to administrators regarding ASG state changes and remediation actions.

---

## 📂 Project Files
- `cloudformation-template.yaml` → AWS CloudFormation template for setting up the infrastructure.
- `lambda-auto-remediation.py` → AWS Lambda function to handle ASG auto-recovery.
- `README.md` → Project documentation.

---

## 🔧 Deployment Steps

1. **Clone the repository:**
   ```sh
   git clone https://github.com/ErkanBarann/AWS-Projects.git
   cd AWS-Projects/auto-remediation
