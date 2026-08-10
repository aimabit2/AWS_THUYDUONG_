---
title: "Tuần 5 - Các nguyên lý mạng trong AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---



### Mục tiêu tuần 5:

Trong Tuần 5, tôi tập trung vào việc triển khai giao diện người dùng và thiết lập khả năng truy vấn serverless cho dự án Financial Data Lake. Tuần làm việc bắt đầu bằng việc thiết lập quy trình triển khai tự động cho frontend sử dụng AWS Amplify, tiếp theo là cấu hình phân phối nội dung toàn cầu và lưu trữ bộ nhớ đệm (caching) qua AWS CloudFront. Cuối cùng, tôi đã cấu hình AWS Athena để thực thi các truy vấn SQL ad-hoc và phân tích trực tiếp trên các tập dữ liệu tài chính thô và đã qua xử lý được lưu trữ trên Amazon S3.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Frontend Deployment with AWS Amplify | Tự động hóa quy trình hosting và CI/CD giúp đẩy nhanh tốc độ chuyển giao tính năng, đồng thời cung cấp môi trường lưu trữ liền mạch cho ứng dụng web. |
| B | Global Distribution & Edge Caching with AWS CloudFront | Tự động hóa quy trình hosting và CI/CD giúp đẩy nhanh tốc độ chuyển giao tính năng, đồng thời cung cấp môi trường lưu trữ liền mạch cho ứng dụng web. |
| C | Serverless Data Analytics with AWS Athena | Truy vấn dữ liệu trên S3 trực tiếp bằng SQL cho phép phân tích dữ liệu hiệu quả về chi phí và đạt hiệu năng cao mà không tốn chi phí quản lý hạ tầng cơ sở dữ liệu. |

### Lĩnh vực A: TRIỂN KHAI FRONTEND VỚI AWS AMPLIFY

#### *Thứ Hai, 20/07 | Thiết lập AWS Amplify & Quy trình CI/CD*
- Cấu hình AWS Amplify để lưu trữ giao diện bảng điều khiển (dashboard) cho việc hiển thị dữ liệu tài chính và trạng thái thực thi của hệ thống.

- Kết nối kho lưu trữ mã nguồn (repository) của dự án để thiết lập quy trình tự động xây dựng và triển khai mỗi khi có cập nhật mã nguồn mới.

- Thiết lập các biến môi trường, cấu hình đóng gói ứng dụng và chiến lược nhánh triển khai cho môi trường thử nghiệm và sản xuất.

- Theo dõi các lượt đóng gói đầu tiên và tối ưu hóa các kịch bản xây dựng nhằm giảm dung lượng tập tin và rút ngắn thời gian triển khai.

> **Kiến thức rút ra:** Tích hợp tự động hóa quy trình CI/CD với AWS Amplify giúp giảm đáng kể chi phí vận hành triển khai và đảm bảo khả năng bàn giao giao diện người dùng một cách nhanh chóng.

#### *Thứ Ba, 21/07 | Quản lý Tên miền tùy chỉnh & Cấu hình Môi trường*
- Cấu hình ánh xạ tên miền tùy chỉnh và tự động cấp phát chứng chỉ bảo mật SSL/TLS thông qua AWS Amplify.

- Thiết lập các quy tắc điều hướng, ghi lại đường dẫn và chuyển hướng cho ứng dụng trang đơn (SPA).

- Tích hợp các điểm đầu kết nối (endpoints) của API Gateway vào cấu hình giao diện người dùng để cho phép thực hiện các lệnh gọi giao diện lập trình an toàn tới dịch vụ hậu cần (backend).
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


