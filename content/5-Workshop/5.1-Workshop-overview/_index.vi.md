---
title : "Overview & System Architecture"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### 5.1 Overview & System Architecture
#### 5.1.1. Bối cảnh và Bài toán nghiệp vụ

Thị trường chứng khoán Việt Nam với hơn 1.600 doanh nghiệp phi tài chính niêm yết trên ba sàn HOSE, HNX và UPCOM đặt ra thách thức lớn trong việc theo dõi và đánh giá sức khỏe tài chính. Dữ liệu báo cáo tài chính từ các nguồn cung cấp thường bị phân tán, bất đồng bộ về tên gọi chỉ tiêu và không nhất quán về định dạng.

Hệ thống được thiết kế nhằm tự động hóa toàn bộ quy trình từ khâu cào dữ liệu thô, chuẩn hóa ETL, lưu trữ Data Lake, tính toán ma trận tỷ số tài chính, cho đến gán nhãn rủi ro kiệt quệ tài chính (Financial Distress) bằng quy định pháp lý Việt Nam kết hợp chỉ số Altman Z-Score. Tập dữ liệu này sau đó được sử dụng để huấn luyện các mô hình học máy (Machine Learning) giúp đưa ra cảnh báo sớm cho nhà đầu tư trước từ 1 đến 2 năm.

#### 5.1.2. Bảng tổng quan các tầng kiến trúc AWS Serverless 5 tầng

| Tầng kiến trúc | Dịch vụ AWS chính | Chức năng kỹ thuật cốt lõi | Chi phí ước tính/tháng |
| :--- | :--- | :--- | :--- |
| **1. Ingestion Layer**  | EventBridge, Step Functions, AWS Lambda  | Lập lịch cron quý/năm, điều phối luồng cào dữ liệu *vnstock* song song qua Lambda, xử lý cơ chế thử lại khi lỗi  | ~$0.30 USD   |
| **2. Data Lake & Storage Layer**  | Amazon S3 (Raw/Curated)  | Lưu trữ tập trung dữ liệu thô (JSON/CSV) và dữ liệu đã chuẩn hóa, dán nhãn (Apache Parquet)  | ~$0.30 USD  |
| **3. AI/ML Layer**  | AWS Glue ETL, Data Catalog, Amazon Athena  | Chạy Glue PySpark Jobs chuẩn hóa schema, Winsorization, tính ma trận tỷ số & Z-Score, crawlers cập nhật catalog và Athena truy vấn SQL  | ~$0.85 USD  |
| **4. REST API & Security Layer**  | Amazon Cognito, API Gateway, AWS WAF, Lambda API  | Quản lý danh tính JWT, định tuyến REST API, chống tấn công web (DDoS, SQLi) và thực thi logic backend  | ~$0.35 USD  |
| **5. Presentation & Alert**  | AWS Amplify, Amazon SES  | Hosting Web Dashboard (React/Next.js) và tự động gửi email cảnh báo rủi ro cho nhà đầu tư  | ~$0.40 USD  |

#### MÔ TẢ VÀ GIẢI THÍCH HÌNH ẢNH 5.1:
![Sơ đồ Kiến trúc Hệ thống 5 tầng trên AWS Cloud.] ()

- Sơ đồ mô tả luồng dữ liệu giữa các dịch vụ Cloud theo kiến trúc Serverless. Bên trái là các nguồn dữ liệu chứng khoán đi qua tầng Ingestion (EventBridge, Step Functions, Lambda) đổ vào S3 Raw Bucket. Tiếp theo, luồng dữ liệu đi qua tầng Processing (AWS Glue Jobs, Data Catalog) sang S3 Curated Bucket và kết nối tới Athena. Tầng REST API & Security (Cognito, API Gateway, WAF, Lambda Backend) đóng vai trò trung gian định tuyến yêu cầu truy vấn. Bên phải sơ đồ là tầng Presentation & Notification hiển thị giao diện phân tích trên AWS Amplify và gửi mail tự động qua Amazon SES.

### 5.2 Automated Data Ingestion Pipeline
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
