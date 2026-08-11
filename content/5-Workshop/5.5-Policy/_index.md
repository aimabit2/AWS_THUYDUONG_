---
title: "Web Dashboard & Alerting (Amplify, Lambda & SES)"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### 5.5 Deploying Web Dashboard & Alerting System (Amplify, Lambda & SES)

#### 5.5 Deploying Web Dashboard & Alerting System (Amplify, Lambda & SES)

The visual Web Dashboard interface visualizes data hosted on AWS Amplify. Combined with this is an automated event processing pipeline that triggers Amazon SES to send email notifications to investors immediately when a company is classified into the high financial risk group.

#### 5.5.2. Triggering Process and Automated Alerting Workflow Table


| Step  | Execution Component | Specific Technical Action |
| :--- | :--- | :--- |
| **1. Incident Detection**| AWS Glue ETL Job | Identifies the distress risk label `distress = 1` upon completing the financial statement calculation period |
| **2. Event Triggering** | Amazon EventBridge / S3 Event | Sends an event message containing the violating ticker symbol information to AWS Lambda |
| **3. Notification Formatting** | AWS Lambda | Extracts subscriber emails, renders HTML templates containing violation reasons & Z-Score metrics |
| **4. Email Dispatch** | Amazon SES (Simple Email Service) | Executes immediate automated warning email dispatch to the investor's inbox |

#### 5.5.3. Step-by-Step Implementation Guide

- **Step 1: Deploy Web Dashboard on AWS Amplify**
  1. Navigate to AWS Amplify Console ➔ Click Host web app.
  2. Connect to the GitHub Repository containing the source code for the Web Dashboard application (React/Next.js).
  3. Configure Build Environment Variables:
    `REACT_APP_API_GATEWAY_URL`: URL of the REST API Gateway prod.
    `REACT_APP_COGNITO_USER_POOL_ID`: User Pool ID.
    `REACT_APP_COGNITO_CLIENT_ID`: App Client ID.
  4. Click **Save and deploy**. AWS Amplify will automatically execute the CI/CD pipeline, package the application, and provision an HTTPS domain for the Web Dashboard.

- **Step 2: Configure Amazon SES (Simple Email Service)**
  1. Navigate to Amazon SES Console ➔ Select Verified identities.
  2. Click Create identity ➔ Select Email address.
  3. Enter the alert recipient Email address (e.g., alert-financial@domain.com).
  4. Access the Email inbox and click the confirmation link sent by AWS SES to complete verification.

- **Step 3: Write AWS Lambda Function to Automatically Send Warning Emails (SES)**
The Lambda source code scans the list of enterprises touching the red threshold of financial distress risk ($Z\text{-score} \le 1.23$) and triggers the Amazon SES service to send emails to investors:

```python
import boto3
import json

ses_client = boto3.client('ses', region_name='ap-southeast-1')
SENDER_EMAIL = "alert-financial@domain.com"

def lambda_handler(event, context):
    # Nhận dữ liệu doanh nghiệp vi phạm từ Glue ETL hoặc Athena Callback
    records = event.get('distress_records', [])
    
    for record in records:
        symbol = record.get('symbol')
        z_score = record.get('z_score')
        year = record.get('year')
        
        subject = f"⚠️ CẢNH BÁO RỦI RO TÀI CHÍNH BÁO ĐỘNG: Mã chứng khoán {symbol} ({year})"
        body_text = f"""
        CẢNH BÁO HỆ THỐNG PHÂN TÍCH RỦI RO TÀI CHÍNH CHỨNG KHOÁN VIỆT NAM
        -------------------------------------------------------------
        Mã doanh nghiệp: {symbol}
        Năm tài chính: {year}
        Chỉ số Altman Z-Score: {z_score} (Đã rơi vào Vạch Đỏ - Distress Zone <= 1.23)
        
        Khuyến nghị: Doanh nghiệp có nguy cơ kiệt quệ tài chính / phá sản cao. Nhà đầu tư nên rà soát kỹ lưỡng danh mục đầu tư.
        """
        
        response = ses_client.send_email(
            Source=SENDER_EMAIL,
            Destination={'ToAddresses': [SENDER_EMAIL]},
            Message={
                'Subject': {'Data': subject, 'Charset': 'UTF-8'},
                'Body': {'Text': {'Data': body_text, 'Charset': 'UTF-8'}}
            }
        )
        print(f"Đã gửi thành công email cảnh báo mã {symbol}, MessageId: {response['MessageId']}")
        
    return {
        'statusCode': 200,
        'body': json.dumps("Đã hoàn tất quy trình gửi Email cảnh báo thành công!")
    }
```
