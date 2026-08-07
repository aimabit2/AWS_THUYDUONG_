---
title : "VPC Endpoint Policies"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

Trong phần này, bạn sẽ tìm hiểu về chính sách VPC Endpoint và cách sử dụng nó để kiểm soát quyền truy cập đến Amazon S3 thông qua điểm cuối.

Khi bạn tạo một Interface Endpoint hoặc Gateway endpoint, bạn có thể đính kèm một chính sách điểm cuối để kiểm soát quyền truy cập vào dịch vụ mà bạn đang kết nối. Chính sách VPC Endpoint là chính sách tài nguyên IAM đính kèm trực tiếp vào điểm cuối. Nếu không đính kèm chính sách tùy chỉnh, AWS sẽ áp dụng chính sách mặc định để cho phép truy cập toàn quyền thông qua điểm cuối.

Bạn có thể tạo chính sách chỉ hạn chế quyền truy cập vào các S3 bucket cụ thể. Điều này hữu ích nếu bạn chỉ muốn một số bucket nhất định có thể truy cập qua điểm cuối.

Trong phần này, bạn sẽ tạo chính sách VPC Endpoint hạn chế quyền truy cập vào một S3 bucket được chỉ định trong chính sách.

![endpoint diagram](/images/5-Workshop/5.5-Policy/s3-bucket-policy.png)

#### Kết nối tới EC2 và xác minh truy cập S3

1. Bắt đầu một phiên AWS Session Manager mới trên máy chủ có tên Test-Gateway-Endpoint.
2. Từ phiên này, xác minh rằng bạn có thể liệt kê nội dung của bucket đã tạo trong phần Truy cập S3 từ VPC.

```
aws s3 ls s3://<your-bucket-name>
```

![test](/images/5-Workshop/5.5-Policy/test1.png)

Nội dung của bucket bao gồm hai tệp có dung lượng 1GB đã được tải lên trước đó.

3. Tạo một bucket S3 mới; tuân thủ mẫu đặt tên mà bạn đã sử dụng trong phần 1, nhưng thêm '-2' vào tên.
4. Mặc định các trường khác và nhấp vào **Create**.

![create bucket](/images/5-Workshop/5.5-Policy/create-bucket.png)

5. Tạo bucket thành công.

![Success](/images/5-Workshop/5.5-Policy/create-bucket-success.png)

Chính sách mặc định cho phép truy cập vào tất cả các S3 bucket thông qua VPC endpoint.

6. Trong giao diện **Edit Policy**, sao chép và dán theo policy sau, thay thế yourbucketname-2 bằng tên bucket thứ hai của bạn. Policy này sẽ cho phép truy cập đến bucket mới qua VPC endpoint, nhưng không cho phép truy cập những bucket khác.

```
{
  "Id": "Policy1631305502445",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1631305501021",
      "Action": "s3:*",
      "Effect": "Allow",
      "Resource": [
                "arn:aws:s3:::yourbucketname-2",
                "arn:aws:s3:::yourbucketname-2/*"
      ],
      "Principal": "*"
    }
  ]
}
```

![custom policy](/images/5-Workshop/5.5-Policy/policy2.png)

Cấu hình policy thành công.

![success](/images/5-Workshop/5.5-Policy/success.png)

7. Từ phiên của bạn trên Test-Gateway-Endpoint instance, kiểm tra truy cập vào bucket đã tạo ở bước đầu.

```
aws s3 ls s3://<yourbucketname>
```

Câu lệnh trả về lỗi vì bucket này không có quyền truy cập qua VPC endpoint policy.

![error](/images/5-Workshop/5.5-Policy/error.png)

8. Tạo file ```fallocate -l 1G test-bucket2.xyz``` và sao chép file lên bucket thứ hai.

```
aws s3 cp test-bucket2.xyz s3://<your-2nd-bucket-name>
```

![success](/images/5-Workshop/5.5-Policy/test2.png)

Thao tác này được cho phép bởi VPC endpoint policy.

![success](/images/5-Workshop/5.5-Policy/test2-success.png)

9. Kiểm tra truy cập vào bucket đầu tiên.

```
aws s3 cp test-bucket2.xyz s3://<your-1st-bucket-name>
```

![fail](/images/5-Workshop/5.5-Policy/test2-fail.png)

Câu lệnh xảy ra lỗi vì bucket không có quyền truy cập bởi VPC endpoint policy.

Trong phần này, bạn đã tạo chính sách VPC Endpoint cho Amazon S3 và sử dụng AWS CLI để kiểm tra chính sách. Các thao tác CLI nhắm vào bucket ban đầu thất bại vì chính sách chỉ cho phép bucket thứ hai. Ngược lại, các thao tác vào bucket thứ hai thành công.
