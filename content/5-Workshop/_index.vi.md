---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# Workshop thực hành: truy cập S3 riêng tư qua VPC Endpoint

#### Tổng quan

Bài lab này biến kiến trúc đã trình bày trong đề xuất và blog thành một triển khai AWS thực tế. Chúng ta sẽ thiết lập kết nối riêng tư đến Amazon S3 bằng Gateway endpoint cho VPC Cloud và Interface endpoint cho môi trường on-premise giả lập, đồng thời chứng minh cách giữ lưu lượng S3 trong mạng riêng của AWS.

#### Mục tiêu

- Triển khai Gateway endpoint cho Amazon S3 trong VPC Cloud.
- Mô phỏng kết nối hybrid từ On-premises qua VPN và PrivateLink.
- Kiểm thử truy cập S3 an toàn mà không qua Internet công cộng.
- Khám phá cơ chế Route 53 Resolver và chính sách VPC Endpoint.

#### Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Truy cập đến S3 từ VPC](5.3-S3-vpc/)
4. [Truy cập đến S3 từ TTDL On-premises](5.4-S3-onprem/)
5. [VPC Endpoint Policies (làm thêm)](5.5-Policy/)
6. [Dọn dẹp tài nguyên](5.6-Cleanup/)
