# 🏗️ Highly Available WordPress Deployment on AWS

## 📌 Project Overview
This project demonstrates a **highly available WordPress deployment** on AWS using a **Virtual Private Cloud (VPC)**. The architecture ensures **scalability, security, and redundancy** by distributing WordPress instances across multiple **Availability Zones (AZs)** with a **Load Balancer** and **Amazon RDS** for database management.

---

## 🚀 Solution Architecture

### 🔹 **VPC (Virtual Private Cloud)**
- The network is configured with a **10.0.0.0/16** CIDR range.
- Subnets are distributed across **two Availability Zones**.

### 🔹 **Public & Private Subnets**
- **Public subnets**: Contain NAT Gateways for outbound internet access.
- **Private subnets**: Host **WordPress EC2 instances** and **Amazon RDS databases**.

### 🔹 **Load Balancer**
- Balances traffic between **WordPress EC2 instances** in different **Availability Zones**.
- Ensures high availability and fault tolerance.

### 🔹 **NAT Gateway**
- Allows outbound internet traffic for private instances while keeping them secure.

### 🔹 **EC2 - WordPress Instances**
- Hosted in private subnets.
- Configured to serve WordPress content and handle requests from the Load Balancer.
- Uses **Security Groups** to allow only necessary traffic.

### 🔹 **Amazon RDS - MySQL Database**
- Stores WordPress content and configurations.
- **Read Replica** is configured for performance and redundancy.
- Placed in a private subnet with strict **Security Group** rules.

---

## 📂 Project Files
- `cloudformation-template.yaml` → Infrastructure as Code (IaC) template for AWS deployment.
- `wordpress-installation.sh` → Script to configure WordPress on EC2 instances.
- `README.md` → Project documentation.

---

## 🔧 Deployment Steps

1. **Clone the repository:**
   ```sh
   git clone https://github.com/ErkanBarann/AWS-Projects.git
   cd AWS-Projects/wordpress-vpc
   ```

2. **Deploy CloudFormation Stack:**
   ```sh
   aws cloudformation create-stack --stack-name WordPressVPCStack --template-body file://cloudformation-template.yaml --capabilities CAPABILITY_NAMED_IAM
   ```

3. **Connect to EC2 Instances & Install WordPress:**
   ```sh
   ssh -i <keyfile.pem> ec2-user@<EC2-Public-IP>
   sudo bash wordpress-installation.sh
   ```

4. **Access WordPress:**
   - Navigate to the **Load Balancer URL** to complete the WordPress setup.

5. **Monitor & Manage Resources:**
   ```sh
   aws rds describe-db-instances
   aws ec2 describe-instances
   aws elbv2 describe-load-balancers
   ```

---

## 📌 Key Benefits
✔️ **High Availability:** Multi-AZ deployment ensures uptime.  
✔️ **Scalability:** Load Balancer supports increased traffic.  
✔️ **Security:** Private subnets restrict unauthorized access.  
✔️ **Performance Optimization:** RDS Read Replica improves database efficiency.  

---

## 📩 Contact & Support
For issues or contributions, feel free to open a GitHub issue or reach out to the DevOps team.

