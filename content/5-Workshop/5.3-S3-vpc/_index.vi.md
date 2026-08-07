---
title : "Truy cập S3 từ VPC"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

#### Workshop narrative

Phần này nối kiến trúc S3 Data Lake từ đề xuất đến một giải pháp AWS cụ thể: Gateway endpoint cho Amazon S3.

Gateway endpoint cho phép các workload trong VPC truy cập S3 mà không đi qua Internet công cộng. Với một nền tảng phân tích tài chính, điều này giúp giảm rủi ro và giữ dữ liệu nhạy cảm trong mạng riêng của AWS.

#### Nội dung

- vai trò của Gateway endpoint trong kiến trúc data lake.
- lợi ích vận hành khi giữ traffic trên hạ tầng nội bộ AWS.
- cấu hình VPC Cloud để dùng S3 riêng tư.

#### Kết luận

Gateway endpoint là cách đơn giản và hiệu quả nhất để kết nối workload VPC với S3 một cách an toàn khi các tài nguyên cùng nằm trong VPC.

#### Trang liên quan

- [Tạo gateway endpoint](5.3.1-create-gwe/)
- [Test gateway endpoint](5.3.2-test-gwe/)
