---
title: "WORKSHOP TRIỂN KHAI HỆ THỐNG"
date: 2026-08-08
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

### 5.1 TỔNG QUAN WORKSHOP
#### 1. TỔNG QUAN

Trong bối cảnh thị trường chứng khoán Việt Nam (HOSE, HNX, UPCOM) phát triển nhanh chóng, dữ liệu báo cáo tài chính của các doanh nghiệp niêm yết thường phân tán, không đồng nhất về cấu trúc và tốn nhiều chi phí xử lý thủ công. Workshop này hướng dẫn từng bước (step-by-step) xây dựng và triển khai **Hệ thống tự động thu thập, phân tích dữ liệu tài chính và dự báo kiệt quệ tài chính (Financial Distress Prediction System)** vận hành hoàn toàn trên kiến trúc **AWS Serverless 5 tầng**.

Hệ thống giúp tự động hóa 100% quy trình từ cào dữ liệu thô, chuẩn hóa ETL, lưu trữ Data Lake, tính toán ma trận tỷ số tài chính, áp dụng mô hình nhãn hóa quy định kết hợp Altman Z-Score và Machine Learning, đến hiển thị trên Web Dashboard và phát tin nhắn cảnh báo sớm cho nhà đầu tư.

- **Đối tượng hướng tới**: Data Engineers, Cloud Architects, Financial Analysts, MLOps Engineers, và sinh viên/nghiên cứu sinh ngành Công nghệ Thông tin / Tài chính.  
- **Chi phí vận hành dự kiến**: ~$1.50 – $3.00 USD/tháng nhờ tối ưu hóa theo mô hình Serverless Pay-as-you-go. 

#### 2. MỤC TIÊU WORKSHOP

Sau khi hoàn thành bài workshop này, người thực hiện sẽ đạt được các mục tiêu chuyên môn sau:

- **Tự động hóa Ingestion Pipeline**: Nắm vững cách sử dụng Amazon EventBridge, AWS Step Functions, và AWS Lambda / ECS Tasks để tự động trích xuất dữ liệu tài chính từ vnstock.

- **Xây dựng Serverless Data Lake & ETL**: Triển khai AWS Glue PySpark Jobs để xử lý làm sạch, loại bỏ các ngành tài chính đặc thù (Ngân hàng, Chứng khoán, Bảo hiểm), xử lý ngoại lệ (Winsorization 1%-99%), chuyển đổi sang định dạng Apache Parquet nén Snappy, và truy vấn siêu tốc với Amazon Athena.

- **Triển khai AI/ML & Feature Store**: Tích hợp Amazon SageMaker Feature Store, Studio, và Serverless Endpoints để huấn luyện, đánh giá (XGBoost, Random Forest, LightGBM) và phục vụ dự báo rủi ro tài chính trực tuyến.

- **Thiết lập API & Bảo mật hệ thống**: Xây dựng cổng RESTful API Gateway bảo vệ bởi AWS WAF, xác thực người dùng phân quyền chi tiết với Amazon Cognito.

- **Trực quan hóa & Cảnh báo thời gian thực**: Triển khai Web Dashboard trên AWS Amplify (React/Next.js) và tự động kích hoạt Amazon SES gửi mail cảnh báo ngay khi doanh nghiệp vào vùng rủi ro.

- **Quản lý & Tối ưu chi phí**: Thực hiện kiểm soát hạ tầng bằng Infrastructure as Code (IaC) và quy trình dọn dẹp tài nguyên (Resource Cleanup) chuẩn xác để tránh phát sinh chi phí ngoài ý muốn.

#### NỘI DUNG

| Mục | Tên bài thực hành | Nội dung chính |
| :--- | :--- | :--- |
| **5.1** | **Overview & System Architecture** | Tổng quan bài toán, mục tiêu, kiến trúc tổng thể 5 tầng trên AWS Cloud và danh mục triển khai. |
| **5.2** | **Automated Data Ingestion Pipeline** | Tạo S3 Raw Buckets, viết script Lambda crawl vnstock, lọc mã phi tài chính, điều phối luồng chạy tự động bằng EventBridge & Step Functions. |
| **5.3** | **Data Processing & Data Lake (AWS Glue ETL, Data Catalog & Athena)** | Tạo S3 Curated Buckets, viết Glue PySpark Jobs chuẩn hóa Schema, Winsorization, tính ma trận chỉ số & Altman Z-Score, chạy Crawlers và truy vấn SQL trên Athena. |
| **5.4** | **REST API & User Authentication (Cognito, API Gateway & Lambda API)** | Cấu hình Cognito User Pools, dựng REST API Gateway tích hợp AWS WAF bảo mật, viết Lambda Backend làm dịch vụ xử lý dữ liệu. |
| **5.5** | **Web Dashboard & Email Alerts (Amplify, Lambda & SES)** | Triển khai giao diện Web Dashboard (React/Next.js) trên AWS Amplify, cấu hình dịch vụ Amazon SES gửi mail cảnh báo tự động khi xuất hiện rủi ro. |
| **5.6** | **Resource Cleanup & Summary** | Quy trình từng bước dọn dẹp, xóa tài nguyên cloud để phòng tránh phát sinh chi phí ngoài ý muốn và tổng kết dự án. |

1. [Tổng quan & Kiến trúc hệ thống](5.1-overview/)
2. [Đường ống thu thập dữ liệu tự động](5.2-Pipeline/)
3. [Data Processing & Data Lake (AWS Glue ETL, Data Catalog & Athena)](5.3-glue-config/)
4. [REST API & User Authentication (Cognito, API Gateway & Lambda API)](5.4-amplify/)
5. [Web Dashboard & Email Alerts (Amplify, Lambda & SES)](5.5-Policy/)
6. [Resource Cleanup & Summary](5.6-Cleanup/)
