---
title : "Đường ống thu thập dữ liệu tự động"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### 5.2 Đường ống thu thập dữ liệu tự động
#### 5.2.1. Khởi tạo S3 Raw Bucket và Quy tắc lọc ngành
Bước đầu tiên trong đường ống thu thập là khởi tạo S3 Raw Bucket đóng vai trò vùng đệm chứa dữ liệu thô dạng JSON/CSV. Hệ thống tích hợp bộ lọc nghiệp vụ tự động loại bỏ mã cổ phiếu thuộc 4 nhóm ngành đặc thù: Ngân hàng, Chứng khoán, Bảo hiểm và Quỹ đầu tư do cấu trúc báo cáo tài chính khác biệt.

#### 5.2.2. Bảng cấu hình thông số kỹ thuật Luồng Ingestion
| Thành phần  | Công nghệ / Tham số   | Mô tả chi tiết thực thi   |
| :--- | :--- | :--- |
| **Môi trường chạy Script** | AWS Lambda (Python 3.11+) | Chạy script đóng gói thư viện vnstock trích xuất trọn bộ 3 BCTC & giá cổ phiếu |
| **Lịch trình kích hoạt** | Amazon EventBridge Cron | Thiết lập cron-job tự động kích hoạt vào cuối mỗi quý/năm |
| **Bộ điều phối Workflow** | AWS Step Functions State Machine | Điều phối song song (Parallel execution), lưu checkpoint và xử lý retry lùi thời gian khi lỗi API|
| **Đích lưu trữ thô** | Amazon S3 Raw Bucket | Lưu trữ dữ liệu thô dạng : *s3://financial-raw-data/ticker/year/quarter/* | 

#### MÔ TẢ VÀ GIẢI THÍCH HÌNH ẢNH 5.2:
![Sơ đồ Điều phối Luồng Thu thập Dữ liệu với AWS Step Functions.] ()

- Hình ảnh hiển thị đồ thị trạng thái (State Machine Graph) của Step Functions. Nút bắt đầu (Start) kích hoạt bước phân tách mã cổ phiếu theo danh sách. Các nhánh song song đại diện cho việc gọi các hàm Lambda cào dữ liệu từ nhiều API khác nhau. Nếu một tác vụ gặp lỗi kết nối, đường dẫn sẽ rẽ sang nhánh Retry_Logic với cơ chế lùi thời gian ngẫu nhiên (exponential backoff) trước khi ghi file JSON/CSV thành công vào S3 Raw.

#### 5.2.3. Hướng dẫn các bước thực hiện
- **Bước 1: Khởi tạo S3 Raw Bucket**
    1. Truy cập vào AWS Management Console ➔ chọn dịch vụ S3.
    2. Nhấp Create bucket.
    3. Đặt tên Bucket: s3-vietnam-financial-raw-data-prod.
    4. Chọn AWS Region: ap-southeast-1 (Singapore).
    5. Giữ nguyên cấu hình mã hóa SSE-S3 (AES-256) và bật tính năng Bucket Versioning.
    6. Nhấp Create bucket. 

- **Bước 2:  Lọc danh sách Doanh nghiệp phi tài chính**
Do cấu trúc Báo cáo Tài chính của ngành ngân hàng và tài chính có bản chất khác biệt hoàn toàn so với doanh nghiệp sản xuất/thương mại, nhóm mình thực hiện lọc bỏ hoàn toàn các nhóm:
    - ❌ Ngân hàng (Banks)
    - ❌ Công ty Chứng khoán (Securities)
    - ❌ Công ty Bảo hiểm (Insurance)
    - ❌ Công ty Tài chính & Quỹ đầu tư
✅ Chỉ giữ lại danh sách doanh nghiệp phi tài chính niêm yết trên 3 sàn HOSE, HNX, UPCOM.

- **Bước 3:  Viết mã nguồn AWS Lambda Ingestor với `vnstock`**
Viết mã nguồn AWS Lambda Ingestor với vnstock
`import json
import boto3
import pandas as pd
from vnstock import financial_report

s3_client = boto3.client('s3')
BUCKET_NAME = 's3-vietnam-financial-raw-data-prod'

def lambda_handler(event, context):
    symbol = event.get('symbol', 'VNM')
    print(f"Bắt đầu cào dữ liệu cho mã: {symbol}")
    
    # 1. Cào Bảng cân đối kế toán
    balance_sheet = financial_report(symbol=symbol, report_type='BalanceSheet', frequency='Yearly')
    # 2. Cào Báo cáo Kết quả Kinh doanh
    income_statement = financial_report(symbol=symbol, report_type='IncomeStatement', frequency='Yearly')
    # 3. Cào Báo cáo Lưu chuyển Tiền tệ
    cash_flow = financial_report(symbol=symbol, report_type='CashFlow', frequency='Yearly')
    
    # Ghi dữ liệu thô vào S3 Raw Bucket
    raw_payload = {
        'symbol': symbol,
        'balance_sheet': balance_sheet.to_dict(orient='records'),
        'income_statement': income_statement.to_dict(orient='records'),
        'cash_flow': cash_flow.to_dict(orient='records')
    }
    
    s3_key = f"raw/yearly/{symbol}_financial_data.json"
    s3_client.put_object(
        Bucket=BUCKET_NAME,
        Key=s3_key,
        Body=json.dumps(raw_payload, ensure_ascii=False),
        ContentType='application/json'
    )
    
    return {
        'statusCode': 200,
        'body': f"Đã lưu thành công dữ liệu thô mã {symbol} vào S3: {s3_key}"
    }`

- **Bước 4: Khởi tạo Workflow điều phối AWS Step Functions & EventBridge**
    1. AWS Step Functions: Tạo State Machine để duyệt qua danh sách danh mục mã cổ phiếu, gọi Lambda Ingestor xử lý song song, hỗ trợ cơ chế Retry khi gặp Rate Limit và tự động ghi log Checkpoint.
    2. Amazon EventBridge Scheduler: Cấu hình quy tắc Cron Job kích hoạt Step Functions định kỳ (ví dụ: vào 00:00 ngày đầu tiên của mỗi tháng) để tự động thu thập báo cáo tài chính quý/năm mới nhất.

![Sơ đồ AWS Step Functions](\static\images\StepFunction.png)

- Ảnh mô tả luồng điều phối Step Functions.

*Mô tả luồng điều phối Step Functions State Machine trong hệ thống:*

- **Khởi chạy Workflow:** Triggers tự động từ Amazon EventBridge Cron Scheduler hoặc gọi thủ công để kích hoạt toàn bộ pipeline dữ liệu.
- **Tác vụ cào & lưu trữ dữ liệu thô:** Gọi AWS Lambda / ECS Ingestor cào dữ liệu BCTC từ `vnstock`, thực hiện checkpointing và lưu file JSON vào `S3 Raw Bucket`.
- **Tác vụ AWS Glue ETL Job:** Step Functions chuyển sang bước gọi tác vụ **AWS Glue StartJobRun**, tự động kích hoạt tiến trình PySpark ETL làm sạch dữ liệu thô, tính toán các chỉ số tài chính ($CR$, $ROA$, $ROE$, $DAR$, $WCTA$) và gán nhãn nguy cơ phá sản **Altman Z-Score**.
- **Cập nhật Catalog & Hoàn tất:** Sau khi Glue Job hoàn tất thành công, Step Functions tiếp tục kích hoạt AWS Glue Crawler quét metadata cập nhật vào Glue Data Catalog. Nếu phát sinh lỗi, hệ thống tự động thực hiện cơ chế Retry và chuyển sang trạng thái cảnh báo Fail State.

