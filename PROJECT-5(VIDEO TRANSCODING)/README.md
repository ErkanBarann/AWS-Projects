# 🎬 Video Transcoding Pipeline with AWS MediaConvert

## 📌 Project Overview
This project implements an automated **video transcoding pipeline** using AWS services. When a **4K video** is uploaded to an **S3 bucket**, a **Lambda function** is triggered to initiate a transcoding job. The video is converted into **1080p and 720p formats** using **AWS MediaConvert (Elastic Transcoder)** and then stored in separate S3 buckets. An **SNS notification** is sent to inform users about the transcoding process.

---

## 🚀 Solution Architecture

### 🔹 **Amazon S3**
- A source **S3 bucket** stores the uploaded 4K video.
- Transcoded videos are stored in separate **S3 buckets** for 1080p and 720p formats.
- A **thumbnail** bucket stores preview images for processed videos.

### 🔹 **AWS Lambda**
- Triggers automatically when a video is uploaded to the source S3 bucket.
- Sends a request to **AWS MediaConvert** to create a transcoding job.

### 🔹 **AWS MediaConvert (Elastic Transcoder)**
- Processes the uploaded video and converts it into **1080p and 720p resolutions**.
- Stores the transcoded versions in dedicated **S3 buckets**.

### 🔹 **Amazon SNS (Simple Notification Service)**
- Notifies users via email when the transcoding job is completed.
- Provides status updates regarding the process.

---

## 📂 Project Files
- `cloudformation-template.yaml` → AWS CloudFormation template for setting up the infrastructure.
- `lambda-video-transcoder.py` → AWS Lambda function to trigger transcoding jobs.
- `README.md` → Project documentation.

---

## 🔧 Deployment Steps

1. **Clone the repository:**
   ```sh
   git clone https://github.com/ErkanBarann/AWS-Projects.git
   cd AWS-Projects/video-transcoding
   ```

2. **Deploy CloudFormation Stack:**
   ```sh
   aws cloudformation create-stack --stack-name VideoTranscodingStack --template-body file://cloudformation-template.yaml --capabilities CAPABILITY_NAMED_IAM
   ```

3. **Deploy the Lambda Function:**
   ```sh
   aws lambda create-function --function-name VideoTranscoder --runtime python3.8 --role <IAM_ROLE_ARN> --handler lambda-video-transcoder.lambda_handler --zip-file fileb://lambda-video-transcoder.zip
   ```

4. **Monitor CloudWatch Logs for Transcoding Status:**
   ```sh
   aws logs tail /aws/lambda/VideoTranscoder --follow
   ```

5. **Test the Solution by Uploading a 4K Video to the S3 Source Bucket** and verify the transcoding process.

---

## 📌 Key Benefits
✔️ **Automates video transcoding** for optimized streaming.  
✔️ **Improves performance** by storing multiple resolutions.  
✔️ **Sends real-time notifications** for job completion.  
✔️ **Scalable and cost-efficient** architecture using AWS serverless services.  

---

## 📩 Contact & Support
For issues or contributions, feel free to open a GitHub issue or reach out to the DevOps team.

