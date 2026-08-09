---
title : "Automated Data Ingestion Pipeline"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

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