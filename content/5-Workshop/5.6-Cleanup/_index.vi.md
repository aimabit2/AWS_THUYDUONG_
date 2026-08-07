---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Dọn dẹp tài nguyên

Xin chúc mừng bạn đã hoàn thành lab này! Trong lab, bạn đã học cách sử dụng các mô hình kiến trúc để truy cập Amazon S3 mà không sử dụng Public Internet.

- Bằng cách tạo Gateway endpoint, bạn đã cho phép giao tiếp trực tiếp giữa EC2 và Amazon S3 mà không đi qua Internet Gateway.
- Bằng cách tạo Interface endpoint, bạn đã mở rộng kết nối S3 đến môi trường truyền thống giả lập thông qua VPN và PrivateLink.

#### Hướng dẫn dọn dẹp

1. Điều hướng đến Hosted Zones trên Route 53. Chọn zone `s3.us-east-1.amazonaws.com`, sau đó xóa zone và xác nhận bằng cách nhập `delete`.

![hosted zone](/images/5-Workshop/5.6-Cleanup/delete-zone.png)

2. Disassociate Route 53 Resolver Rule `myS3Rule` khỏi VPC Onprem và xóa rule.

![hosted zone](/images/5-Workshop/5.6-Cleanup/vpc.png)

3. Mở CloudFormation console và xóa hai stack đã tạo cho bài lab:
   - `PLOnpremSetup`
   - `PLCloudSetup`

![delete stack](/images/5-Workshop/5.6-Cleanup/delete-stack.png)

4. Xóa các S3 bucket đã tạo cho lab:
   - Mở S3 console.
   - Chọn bucket và đảm bảo nó rỗng.
   - Xóa bucket và xác nhận.

![delete s3](/images/5-Workshop/5.6-Cleanup/delete-s3.png)
