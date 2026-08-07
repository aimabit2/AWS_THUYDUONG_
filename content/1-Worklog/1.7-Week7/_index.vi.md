---
title: "Tuần 7 -Triển khai bảo mật đám mây, giám sát và phát hiện mối đe dọa "
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---



### Mục tiêu tuần 7:

Trong Tuần 7, tôi tập trung vào việc triển khai giám sát toàn diện, phát hiện mối đe dọa, quản lý bí mật và bảo mật lớp biên cho dự án Hồ dữ liệu Tài chính (Financial Data Lake). Tuần làm việc bắt đầu bằng việc thiết lập hệ thống ghi nhật ký tập trung, chỉ số hiệu năng và hệ thống cảnh báo tự động bằng Amazon CloudWatch. Tiếp theo, tôi bật nhật ký kiểm toán với AWS CloudTrail và cấu hình tự động phát hiện mối đe dọa qua AWS GuardDuty. Cuối cùng, tôi bảo mật các thông tin xác thực nhạy cảm bằng AWS Secrets Manager và triển khai các quy tắc AWS WAF để bảo vệ các điểm đầu cuối ứng dụng khỏi các khai phá web phổ biến.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Khả năng Quan sát System & Giám sát với CloudWatch | Tập trung hóa nhật ký và chỉ số giúp tăng khả năng quan sát vận hành theo thời gian thực và chủ động phát hiện sự cố trên hạ tầng đám mây. |
| B | Nhật ký Kiểm toán & Phát hiện Đe dọa với CloudTrail & GuardDuty | Kiểm toán lệnh gọi API liên tục và phân tích mối đe dọa thông minh giúp cải thiện đáng kể mức độ an toàn bảo mật và tuân thủ quy định. |
| C | Quản lý Bí mật & Bảo vệ Lớp biên với Secrets Manager & WAF | Tập trung hóa thông tin xác thực nhạy cảm và lọc lưu lượng web độc hại giúp bảo vệ tính toàn vẹn dữ liệu và ngăn chặn truy cập trái phép. |

### Lĩnh vực A: KHẢ NĂNG QUAN SÁT HỆ THỐNG & GIÁM SÁT VỚI CLOUDWATCH

#### *Thứ Hai, 03/08 | Cấu hình Nhật ký Tập trung & Bảng điều khiển Tùy chỉnh*
- Cấu hình CloudWatch Log Groups và Log Streams để thu thập nhật ký ứng dụng và hạ tầng trên toàn bộ các dịch vụ.

- Tạo các chỉ số CloudWatch tùy chỉnh để giám sát lượng dữ liệu thu thập, tỷ lệ lỗi API và độ trễ hệ thống.

- Xây dựng các Bảng điều khiển CloudWatch tương tác để trực quan hóa sức khỏe của Hồ dữ liệu, hiệu năng hệ thống và các chỉ số vận hành thực tế.

- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Việc gộp các luồng nhật ký và thiết lập bảng điều khiển tùy chỉnh giúp đơn giản hóa quá trình gỡ lỗi hệ thống và đẩy nhanh tốc độ khắc phục sự cố vận hành.

#### *Thứ Ba, 28/07 | Khởi tạo Tự động Môi trường Staging & Production*
- Triển khai hạ tầng mạng cơ bản, lưu trữ và các vai trò IAM thông qua việc thực thi tự động các CloudFormation stacks.

- Cấu hình tính năng phát hiện sai lệch (drift detection) để nhận diện và khắc phục các thay đổi cấu hình thủ công nằm ngoài khung IaC.

- Đánh giá việc quản lý trạng thái Terraform dạng mô-đun so với các CloudFormation stacks lồng nhau cho các kiến trúc nhiều tầng.

- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Việc tự động hóa quản lý SSL và cấu hình điều hướng giúp đơn giản hóa quy trình thiết lập tên miền tùy chỉnh, đồng thời giữ cho giao tiếp ứng dụng luôn an toàn.

### Lĩnh vực B: PHÂN PHỐI TOÀN CẦU & LƯU TRỮ ĐỆM BIÊN VỚI AWS CLOUDFRONT

#### *Thứ Tư, 22/07 | Thiết lập Phân phối CloudFront & Cấu hình Nguồn dữ liệu*
- Tạo mạng phân phối AWS CloudFront để lưu bộ nhớ đệm các tài nguyên tĩnh của giao diện người dùng và tăng tốc độ phân phối phản hồi từ các điểm kết nối API.

- Cấu hình các nguồn dữ liệu gốc trong CloudFront trỏ tới các ngăn chứa dữ liệu S3 (S3 buckets) và các điểm đầu kết nối tùy chỉnh của API Gateway.

- Triển khai Quyền kiểm soát Truy cập Nguồn gốc (OAC) để giới hạn quyền truy cập trực tiếp vào ngăn chứa S3, bắt buộc lưu lượng truy cập phải đi qua CloudFront nhằm tăng cường bảo mật.
- Tài liệu tham khảo: 
> **Kiến thức rút ra:** Bảo vệ nguồn dữ liệu S3 bằng Quyền kiểm soát Truy cập Nguồn gốc CloudFront giúp thực thi chính sách bảo mật điểm vào duy nhất, đồng thời giảm độ trễ cho người dùng cuối trên toàn cầu.

#### *Thứ Năm, 23/07 | Tối ưu hóa Hành vi Bộ nhớ đệm & Chiến lược Xóa Đệm*
- Định nghĩa các hành vi bộ nhớ đệm tùy chỉnh dựa trên mẫu đường dẫn tài nguyên dành riêng cho tài nguyên tĩnh và các điểm kết nối API động.

- Cấu hình thiết lập thời gian tồn tại (TTL) và chính sách khóa bộ nhớ đệm để tối ưu hóa tỷ lệ trúng đệm tại các vị trí biên.

- Thực thi và kiểm thử việc xóa bộ nhớ đệm khi cập nhật các tài nguyên tĩnh trên giao diện người dùng.

- Đánh giá hiệu quả cải thiện hiệu năng khi sử dụng nén dữ liệu CloudFront (Gzip/Brotli) và định tuyến theo vị trí biên.
- Tài liệu tham khảo: 
> **Kiến thức rút ra:** Việc tùy chỉnh hành vi bộ nhớ đệm theo từng loại tài nguyên giúp ngăn ngừa tình trạng dữ liệu cũ, đồng thời tối đa hóa tốc độ phản hồi cho các tài nguyên tĩnh.

### Lĩnh vực C: PHÂN TÍCH DỮ LIỆU KHÔNG MÁY CHỦ VỚI AWS ATHENA

#### *Thứ Sáu, 24/07 | Định nghĩa Lược đồ Athena & Tối ưu hóa Truy vấn Linh hoạt*
- Tích hợp các bảng trong Danh mục Dữ liệu Glue (Glue Data Catalog) với AWS Athena để truy vấn dữ liệu tài chính lớp thô (Bronze) và lớp sạch (Silver) trong các ngăn chứa S3.

- Thực thi các truy vấn SQL linh hoạt để kiểm tra tính nhất quán của dữ liệu đã thu thập, độ lệch lược đồ và định dạng dữ liệu trên toàn bộ bản ghi lịch sử.

- Cấu hình vị trí xuất kết quả, mã hóa kết quả truy vấn và phân quyền nhóm làm việc để quản lý chi phí truy vấn cũng như quyền truy cập.

- Kiểm thử kỹ thuật chiếu phân vùng dữ liệu và định dạng lưu trữ dạng cột (Parquet) để giảm thiểu dung lượng dữ liệu cần quét, giúp tăng tốc độ thực thi truy vấn.
- Tài liệu tham khảo: 
> *Kiến thức rút ra:* Kết hợp Danh mục Dữ liệu Glue với Athena cho phép phân tích dữ liệu tức thì bằng SQL trên Hồ Dữ liệu S3, đồng thời tối ưu hóa chi phí nhờ phân vùng dữ liệu hợp lý.

### Kết quả đạt được
- Triển khai thành công giao diện người dùng của dự án bằng AWS Amplify tích hợp quy trình tự động hóa CI/CD.

- Thiết lập hệ thống phân phối nội dung toàn cầu với AWS CloudFront, bảo vệ các nguồn tài nguyên gốc bằng Quyền kiểm soát Truy cập Nguồn gốc.

- Tối ưu hóa chiến lược lưu bộ nhớ đệm tài nguyên tĩnh, nén dữ liệu phản hồi và xóa đệm trên các vị trí biên.

- Cấu hình AWS Athena để thực thi các truy vấn SQL không máy chủ trực tiếp trên dữ liệu tài chính thô và dữ liệu đã qua xử lý lưu tại S3.

- Giảm thiểu chi phí truy vấn phân tích và độ trễ bằng cách cấu hình tích hợp Danh mục Dữ liệu Glue cùng cấu trúc phân vùng trên S3.




