# AWS Projects 🚀

This repository contains various AWS-based projects. Each project addresses a specific use case and demonstrates how to implement it using different AWS services.

Projects are organized into separate folders, and each folder contains its own `README.md` file.

## 📂 Project List

| # | 📌 Project Name | Description |
|---|-----------------|-------------|
| 1 | Flask Deployment - Auto Scaling & Load Balancer | Deploying a Flask-based Python application on AWS using EC2, ALB, and Auto Scaling Group. |
| 2 | Wordpress on RDS | Deploying a WordPress application using Amazon RDS for database management. |
| 3 | Scalable Contact List App with AWS CloudFormation | Deploying a contact list application using EC2, RDS (MySQL), ALB, Auto Scaling, and CloudFormation. |
| 4 | Highly Available VPC Deployment for WordPress | Deploying a VPC with public & private subnets, IGW, NAT Gateway, and Security Groups for a scalable WordPress setup. |
| 5 | Video Transcoding Pipeline with AWS MediaConvert | A 4K video is uploaded into an S3 bucket. A Lambda function is triggered to create a transcoding job with AWS MediaConvert, converting the video into 1080p and 720p formats and storing them in separate S3 buckets. SNS notifications inform about the transcoding process. |
| 6 | Auto-Remediation for ASG Desired Capacity | APro-Soft uses a 'multiple environment to a single AWS account' approach for EC2 deployments. Due to accidental configuration changes by junior engineers setting the desired capacity of the production ASG to 0, an auto-remediation solution is implemented to automatically restore the correct configuration without modifying IAM permissions. |

## 💡 How to Use
1. Click on a project to view detailed documentation.
2. Clone the repository using:
   ```sh
   git clone https://github.com/ErkanBarann/AWS-Projects.git
   ```

