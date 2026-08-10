---
title: "Tuần 2 - Nền tảng AWS về Lưu trữ, Điện toán, Mạng và Data Engineering"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---


### Tổng quan Tuần 2:

Trong tuần này, tôi tập trung tìm hiểu các dịch vụ cốt lõi của AWS về lưu trữ, điện toán và mạng, đồng thời bắt đầu triển khai dự án Data Engineering của nhóm.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Nền tảng AWS về Lưu trữ và Điện toán | Amazon S3 và Amazon EC2 là những dịch vụ cốt lõi giúp xây dựng hệ thống lưu trữ dữ liệu có khả năng mở rộng và cung cấp tài nguyên tính toán linh hoạt. |
| B | Mạng AWS và Kết nối Hybrid | Một kiến trúc VPC được thiết kế hợp lý cùng với các lớp bảo mật phù hợp là nền tảng của các hệ thống hybrid an toàn. |
| C | Khởi động Dự án Data Engineering | Xây dựng kiến trúc ETL rõ ràng và pipeline thu thập dữ liệu trên môi trường cục bộ tạo tiền đề thuận lợi cho việc triển khai lên Cloud trong tương lai. |

### Lĩnh vực A: Nền tảng AWS về Lưu trữ và Điện toán

#### *Thứ Hai, 29/06 | Amazon S3, Data Lake và Data Warehouse*
- Tìm hiểu **Amazon S3** là dịch vụ lưu trữ đối tượng (Object Storage) có khả năng mở rộng cao của AWS
- Phân biệt vai trò của **Amazon S3**, **Data Lake** và **Data Warehouse** trong các kiến trúc dữ liệu hiện đại
- Tìm hiểu các khái niệm và **Bucket** và **Object**, cách tổ chức dữ liệu, metadata, cơ chế kiểm soát truy cập và các trường hợp sử dụng phổ biến trong doanh nghiệp như sao lưu dữ liệu, phân tích dữ liệu lớn (Big Data Analytics) và xây dựng Data Lake
- So sánh mô hình lưu trữ dữ liệu có cấu trúc dành cho phân tích (**Data Warehouse**) với kho ưu trữ dữ liệu thô (**Data Lake**) để hiểu vai trò của từng mô hình trong quy trình Data Engineering
- Tài liệu tham khảo:
> **Kiến thức rút ra**: Amazon S3 là nền tảng lưu trữ chính để xây dựng Data Lake có khả năng mở rộng, trong khi Data Warehouse tập trung vào việc tối ưu hiện suất phân tích các dữ liệu đã được xử lý.

#### *Thứ Ba, 30/06 | Amazon EC2 và Triển khai Website Tĩnh*
- Tìm hiểu các kiến thức cơ bản về Amazon EC2, bao gồm:
  - Các loại EC2 Instance
  - Key Pair
  - Security Group
  - Quy trình triển khai ứng dụng trên EC2
- Tìm hiểu cách khởi tạo và quản lý các máy chủ ảo trên AWS
- Thực hành triển khai một website tĩnh bằng Amazon S3 nhằm hiểu cách lưu trữ và phân phối website mà không cần sử dụng máy chủ web chuyên dụng
- Tài liệu tham khảo:
> Kiến thức rút ra: Amazon EC2 cung cấp tài nguyên tính toán linh hoạt, trong khi Amazon S3 là giải pháp hiệu quả về chi phí và có tính sẵn sàng cao để triển khai các website tĩnh.

### Lĩnh vực B: Mạng AWS và Kết nối Hybrid

#### *Thứ Tư, 01/07 | Amazon VPC và AWS Site-to-Site VPN*
- Tìm hiểu **Amazon Virtual Private Cloud (VPC)**, bao gồm:
  - CIDR Planning.
  - Regions.
  - Availability Zones.
  - Subnets.
  - Route Tables.
  -  Internet Gateway (IGW).
  - Security Groups.
  -Network ACLs.
- Nghiên cứu các chiến lược phân chia Subnet theo mô hình:
  - Public Subnet.
  - Private Subnet.
  - VPN-only Subnet.
- Thực hành thiết lập kết nối an toàn giữa hệ thống On-premises và AWS Cloud thông qua **AWS Site-to-Site VPN**.
- Tài liệu tham khảo:
> **Kiến thức rút ra**: Một kiến trúc VPC được thiết kế tốt, kết hợp với nhiều lớp bảo mật và kết nối hybrid an toàn sẽ tạo nền tảng cho các hệ thống Cloud có tính sẵn sàng và bảo mật cao.

### Lĩnh vực C: Khởi động Dự án Data Engineering

#### *Thứ Năm, 02/07 | Lập kế hoạch Dự án và Thiết kế Kiến trúc Pipeline*
- Chính thức bắt đầu dự án **Data Engineering** của nhóm.
- Tham gia thảo luận để phân tích mục tiêu nghiệp vụ, kiến trúc hệ thống và lộ trình triển khai của dự án.
- Thiết kế quy trình ETL tổng thể bao gồm các tầng:
  - **Data Ingestion**
  - **Bronze (Raw JSON)**
  - **Silver (Clean Parquet)**
  - **Gold (Feature Engineering)**
  - **Data Validation**
  - **Analytics**
- Rà soát cấu trúc dự án, phân công nhiệm vụ phát triển và xây dựng định hướng triển khai lên môi trường Cloud trong các giai đoạn tiếp theo.
- Tài liệu tham khảo:

####  *Thứ Sáu, 03/07 | Thu thập Dữ liệu Cục bộ với VNStock3*
- Cấu hình môi trường phát triển cục bộ bằng cách cài đặt **VNStock3** và **Pandas**.
- Xây dựng script Python đầu tiên để thu thập dữ liệu thị trường chứng khoán Việt Nam từ VNStock3.
- Thực thi thành công pipeline ETL đầu tiên trên môi trường cục bộ bằng cách lưu dữ liệu thô vào tầng Bronze, trước khi tiếp tục các bước làm sạch dữ liệu, kiểm tra chất lượng và tạo đặc trưng.
- Rà soát kiến trúc pipeline và thảo luận về kế hoạch triển khai lên các dịch vụ AWS trong tương lai.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Việc phân chia pipeline thành các tầng **Bronze**, **Silver** và **Gold** giúp nâng cao chất lượng dữ liệu, tăng khả năng bảo trì và mở rộng hệ thống, đồng thời tạo nền tảng cho việc triển khai theo kiến trúc Cloud-Native.

### Kết quả đạt được
- Hiểu rõ các dịch vụ cốt lõi của AWS bao gồm Amazon S3, Amazon EC2, Amazon VPC và AWS Site-to-Site VPN.
- Tích lũy kinh nghiệm trong việc thiết kế kiến trúc mạng Cloud an toàn và kết nối hybrid theo các khuyến nghị của AWS.
- Chính thức khởi động dự án Data Engineering của nhóm và triển khai thành công giai đoạn đầu của pipeline ETL trên môi trường cục bộ bằng VNStock3.
- Xây dựng nền tảng kỹ thuật cho việc triển khai hệ thống lên AWS trong tương lai bằng cách kết hợp kiến thức về hạ tầng Cloud với quy trình Data Engineering thực tế.

