---
title : "Triển khai Web Dashboard & Hệ thống Cảnh báo (Amplify, Lambda & SES)"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

### 5.5 Triển khai Web Dashboard & Hệ thống Cảnh báo (Amplify, Lambda & SES)
#### 5.5.1. Triển khai giao diện và Hệ thống thông báo
Giao diện Web Dashboard trực quan hóa dữ liệu được lưu trữ trên AWS Amplify. Kết hợp với đó là đường ống xử lý sự kiện tự động kích hoạt Amazon SES gửi mail thông báo cho nhà đầu tư ngay khi doanh nghiệp bị xếp vào nhóm nguy cơ tài chính cao.

#### 5.5.2. Bảng quy trình kích hoạt và xử lý Cảnh báo tự động
| Bước  | Thành phần thực thi   | Hành động kỹ thuật cụ thể |
| :--- | :--- | :--- |
| **1. Phát hiện sự cố**| AWS Glue ETL Job | Xác định nhãn rủi ro distress = 1 sau khi hoàn tất kỳ tính toán BCTC |
| **2. Kích hoạt sự kiện** | Amazon EventBridge / S3 Event | Gửi thông điệp sự kiện chứa thông tin mã cổ phiếu vi phạm đến AWS Lambda |
| **3. Định dạng thông báo** | AWS Lambda | Trích xuất email người theo dõi, render template HTML chứa lý do vi phạm & chỉ số Z-Score |
| **4. Gửi Mail** | Amazon SES (Simple Email Service) | Thực thi gửi email cảnh báo tự động tức thì đến hộp thư nhà đầu tư |

#### 5.5.3. Hướng dẫn các bước thực hiện
- **Bước 1: Deploy Web Dashboard trên AWS Amplify**
  1. Truy cập AWS Amplify Console ➔ Nhấp Host web app.
  2. Kết nối với GitHub Repository chứa mã nguồn ứng dụng Web Dashboard (React/Next.js).
  3. Cấu hình các biến môi trường Build (Environment Variables):
      `REACT_APP_API_GATEWAY_URL`: URL của REST API Gateway `prod`.
      `REACT_APP_COGNITO_USER_POOL_ID`: User Pool ID.
      `REACT_APP_COGNITO_CLIENT_ID`: App Client ID.
  4. Nhấp **Save and deploy**. AWS Amplify sẽ tự động thực thi luồng CI/CD, đóng gói ứng dụng và cấp phát tên miền HTTPS cho Web Dashboard.

- **Bước 2:  Cấu hình Amazon SES (Simple Email Service)**
  1. Vào Amazon SES Console ➔ chọn Verified identities.
  2. Nhấp Create identity ➔ chọn Email address.
  3. Nhập địa chỉ Email nhận cảnh báo (ví dụ: alert-financial@domain.com).
  4. Truy cập hộp thư Email bấm xác nhận liên kết từ AWS SES để hoàn tất verify.

- **Bước 3:  Viết AWS Lambda Function tự động gửi Email Cảnh báo (SES)**
Mã nguồn Lambda quét danh sách doanh nghiệp chạm vạch đỏ rủi ro kiệt quệ tài chính ($Z\text{-score} \le 1.23$) và kích hoạt dịch vụ Amazon SES gửi email tới nhà đầu tư:

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

