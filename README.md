## AWS Lambda Word Count Automation

### Project Title  
**Serverless Word Count Automation using AWS Lambda, S3, and SNS**

---
### Project Diagram

<img width="1672" height="941" alt="AWS Lambda Word Count Automation" src="https://github.com/user-attachments/assets/52f0216c-5467-487f-9281-5303eaefb887" />

---
### Project Overview

This project demonstrates a serverless document-processing workflow using **AWS Lambda, Amazon S3, and Amazon SNS**.  
When a text file is uploaded to an S3 bucket, an AWS Lambda function is automatically triggered to read the file, count the number of words, and send the result as a notification through Amazon SNS.

---
### Solution Overview
- AWS Lambda function written in Python to process uploaded files.
- Amazon S3 bucket configured to trigger Lambda on file upload.
- Amazon SNS topic created to notify subscribers via email/SMS.
- IAM Role (LambdaAccessRole) used to grant permissions for S3, SNS, and CloudWatch.

---
### Project Workflow
A user uploads a .txt file to an Amazon S3 bucket.
The S3 upload event triggers an AWS Lambda function.
The Lambda function reads the uploaded file.
The function calculates the total word count.
The result is sent to an email subscriber using Amazon SNS.
CloudWatch stores logs for monitoring and troubleshooting.
   
---
### Technologies Used

![AWS Lambda](https://img.shields.io/badge/AWS-Lambda-FF9900?style=for-the-badge&logo=awslambda&logoColor=white)
![Amazon S3](https://img.shields.io/badge/Amazon-S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white)
![Amazon SNS](https://img.shields.io/badge/Amazon-SNS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![IAM](https://img.shields.io/badge/AWS-IAM-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white)
![CloudWatch](https://img.shields.io/badge/Amazon-CloudWatch-FF4F8B?style=for-the-badge&logo=amazoncloudwatch&logoColor=white)
![Python](https://img.shields.io/badge/Python-Basic-3776AB?style=for-the-badge&logo=python&logoColor=white)

---
### Technical Implementation
- S3 Bucket: Configured for event notifications.
- SNS Topic: Subscriptions confirmed via email.
- Lambda Function: Python 3.x runtime.

---
### Core Code 

    import json
    import boto3

    def lambda_handler(event, context):
    s3 = boto3.client("s3")
    sns = boto3.client("sns")

    bucket = event["Records"][0]["s3"]["bucket"]["name"]
    key = event["Records"][0]["s3"]["object"]["key"]

    data = s3.get_object(Bucket=bucket, Key=key)
    contents = data["Body"].read()

    total_words = contents.split()
    message = f"The word count in the file {key} is {len(total_words)}"

    snsArn = "paste-your-sns-topic-arn-here"
    sns.publish(
        TopicArn=snsArn,
        Message=message,
        Subject="Word Count Result"
    )

---
### Testing & Validation
-	Uploaded multiple text files with varying lengths.
-	Verified email notifications with accurate word counts.
-	Logs monitored in CloudWatch for debugging and validation.
---
### Key Deliverables
-	Lambda function deployed and tested.
-	S3 bucket with trigger configured.
-	SNS topic with confirmed subscription.
-	Email notification screenshot.
-	Documentation of steps and architecture diagram.
---
### Impact & Learning
-	Demonstrated event driven serverless architecture.
-	Hands on experience with AWS Lambda, S3, SNS, IAM, CloudWatch.
-	Reinforced skills in Python automation and cloud integration.
-	Project showcasing AWS serverless expertise.
