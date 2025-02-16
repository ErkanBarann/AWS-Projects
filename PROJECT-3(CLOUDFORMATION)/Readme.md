# 📌 Contact List Application  

## 📖 Overview  
This project is a **scalable Contact List Application** deployed on AWS using **EC2, RDS (MySQL), Load Balancer, and Auto Scaling**. The deployment is managed through **AWS CloudFormation**, which automates the infrastructure provisioning.  

## 🏗 Architecture  
The application follows a **highly available and scalable** architecture:  
- **VPC & Public Subnet**: The infrastructure is deployed inside a Virtual Private Cloud (VPC) with public subnets.  
- **EC2 Instances (Auto Scaling Group)**: The application is hosted on EC2 instances that automatically scale based on traffic.  
- **Application Load Balancer (ALB)**: Balances incoming traffic among EC2 instances.  
- **Amazon RDS (MySQL)**: A managed database service for storing contact list data.  
- **Security Groups**: Control inbound and outbound network traffic.  
- **AWS Route 53**: Manages domain name resolution and routing.  
- **AWS CloudFormation**: Automates the provisioning of AWS infrastructure using templates.  
- **GitHub Integration**: The CloudFormation template is stored in a GitHub repository for easy deployment and version control.  

## 🚀 Deployment Steps  
### **1️⃣ Prerequisites**  
Before deploying this project, make sure you have:  
- An **AWS account** with IAM permissions  
- **AWS CLI** installed and configured  
- **CloudFormation template** stored in your GitHub repository  

### **2️⃣ Clone the Repository**  
```bash
git clone https://github.com/your-github-repo/contact-list-app.git
cd contact-list-app```

3️⃣ Deploy Using CloudFormation
Run the following command to create the stack:

```bash
aws cloudformation create-stack --stack-name ContactListApp \
    --template-body file://cloudformation-template.yaml \
    --capabilities CAPABILITY_IAM```


4️⃣ Check Deployment Status

Monitor the stack creation process in the AWS Console under CloudFormation → Stacks.

5️⃣ Access the Application

Once the deployment is complete, retrieve the Load Balancer URL from the output section of CloudFormation and access it via a browser:
```bash
echo "Your application is available at: http://$(aws cloudformation describe-stacks --stack-name ContactListApp --query "Stacks[0].Outputs[?OutputKey=='LoadBalancerDNSName'].OutputValue" --output text)"```


🛠 Technologies Used

AWS EC2 (Elastic Compute Cloud)
AWS RDS (MySQL)
AWS Auto Scaling Group
AWS Application Load Balancer (ALB)
AWS CloudFormation
AWS Route 53
GitHub (for storing CloudFormation templates)

📌 Future Enhancements

Implement CI/CD pipeline using AWS CodePipeline & GitHub Actions.
Add IAM Role-based access control for enhanced security.
Enable CloudWatch monitoring for real-time logging and alerts.