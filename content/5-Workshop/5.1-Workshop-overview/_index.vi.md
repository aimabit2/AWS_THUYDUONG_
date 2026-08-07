---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Tóm tắt

Workshop này chuyển đổi kiến trúc dữ liệu của hệ thống dự báo tài chính thành một minh họa AWS thực tế. Bạn sẽ học cách giữ đường dẫn dữ liệu đến Amazon S3 nằm trong mạng riêng không gian AWS, đồng thời mô phỏng truy cập từ môi trường on-premise qua VPN và PrivateLink.

#### Nội dung chính

- Mô hình VPC Cloud chứa workload điện toán và S3 Data Lake.
- Mô phỏng VPC On-Prem dùng VPN để truy cập S3 qua Interface endpoint.
- Sử dụng Gateway endpoint để giữ traffic S3 trong AWS khi chạy trên VPC.
- Xây dựng một giải pháp hybrid riêng tư dành cho dữ liệu nhạy cảm.

#### Kiến trúc

![overview](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)

Kiến trúc workshop bao gồm:
- **VPC Cloud**: môi trường AWS chứa EC2 và tài nguyên truy cập S3.
- **VPC On-Prem**: mô phỏng dữ liệu nội bộ kết nối qua VPN.
- **Amazon S3**: Data Lake trung tâm cho dữ liệu tài chính.
- **VPC Endpoints**: Gateway và Interface endpoints giúp bảo vệ lưu lượng S3.
