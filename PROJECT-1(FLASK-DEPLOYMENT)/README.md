# **AWS Flask Deployment - Auto Scaling and Load Balancer**

## **Project Description**
This project aims to deploy a Flask-based Python application on AWS. The architecture will be built using **Auto Scaling Group, Application Load Balancer, and EC2 instances**. The source code will be pulled from GitHub, and the Flask application will be automatically launched.

## **Architectural Components**
- **VPC (Virtual Private Cloud)**: Creates an isolated network.
- **Public Subnet**: The network component that will host EC2 instances.
- **EC2 Instances**: Virtual machines running the Flask application.
- **Auto Scaling Group**: Scales EC2 instances based on traffic demand.
- **Application Load Balancer**: Distributes traffic evenly.
- **Security Groups**: Defines firewall rules.
- **GitHub**: Repository for managing source code.

## **Requirements**
- AWS Account
- Access to AWS Management Console
- GitHub Account
- A simple Python application using Flask

---

## **1. Creating AWS Resources**

### **1.1 Defining VPC and Subnet (AWS Management Console)**
1. The default VPC and subnets will be used.

### **1.2 Configuring Security Groups**
1. Security groups will be created for both EC2 instances and the ALB.
   - **EC2 Security Group** inbound rules: `SSH: Anywhere` and `HTTP: ALB Security Group`
   - **ALB Security Group** inbound rules: `HTTP: Anywhere`

### **1.3 Creating Load Balancer and Target Group**
1. Configure the necessary settings to create the **Application Load Balancer** and **Target Group**.

---

## **2. Launching EC2 Instances**

### **2.1 Setting Up Flask with a Launch Template**
- Go to **EC2 Dashboard** > **Launch Templates**.
- Click **Create Launch Template**.
- Select **Ubuntu 24.04** as the **Amazon Machine Image (AMI)**.
- Choose **t2.micro** as the **Instance Type**.
- Attach the **Security Group** you created.
- Under the **User Data** section, add the following script:

```bash
#!/bin/bash
apt update -y
apt install git python3-pip python3-flask -y
cd /home/ubuntu
git clone https://github.com/your_github_repo/flask_app.git
cd flask_app
python3 app.py
