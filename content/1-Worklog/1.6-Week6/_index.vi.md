---
title: "Tuần 6 - Tự động hóa Hạ tầng & Chuyển giao Liên tục trên AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Mục tiêu tuần 6:

Trong Tuần 6, tôi tập trung vào việc tự động hóa hạ tầng và thiết lập quy trình tích hợp và chuyển giao liên tục (CI/CD) cho dự án Hồ dữ liệu Tài chính (Financial Data Lake). Tuần làm việc bắt đầu bằng việc định nghĩa Hạ tầng dưới dạng Mã (IaC) sử dụng các mẫu Terraform và AWS CloudFormation. Tiếp theo, tôi cấu hình các chính sách truy cập chi tiết bằng AWS IAM và tổ chức các lớp lưu trữ dữ liệu tự động trên Amazon S3. Cuối cùng, tôi xây dựng các pipeline triển khai hoàn toàn tự động sử dụng AWS CodePipeline và AWS CodeBuild để tối ưu hóa việc cập nhật ứng dụng và khởi tạo hạ tầng.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Hạ tầng dưới dạng Mã (IaC) với Terraform & CloudFormation | Khai báo hạ tầng đám mây bằng mã nguồn giúp đảm bảo việc triển khai nhất quán, có thể lặp lại và quản lý theo phiên bản trên các môi trường. |
| B | Quản lý Truy cập & Lưu trữ với IAM & Amazon S3 | Triển khai các chính sách IAM đặc quyền tối thiểu kết hợp với các phân lớp lưu trữ S3 giúp đảm bảo an toàn dữ liệu và quản lý vòng đời hiệu quả. |
| C | Pipeline CI/CD Tự động với AWS CodePipeline & CodeBuild | Tự động hóa quy trình đóng gói, kiểm thử và triển khai giúp đẩy nhanh chu kỳ phát hành và loại bỏ các lỗi cấu hình thủ công. |

### Lĩnh vực A: HẠ TẦNG DƯỚI DẠNG MÃ (IaC) VỚI TERRAFORM & CLOUDFORMATION

#### *Thứ Hai, 27/07 | Mô-đun hóa Hạ tầng với Terraform & CloudFormation*
- Viết các mô-đun Terraform và mẫu AWS CloudFormation để khởi tạo các tài nguyên hạ tầng đám mây bằng mã lập trình.

- Thiết lập chiến lược quản lý trạng thái (state) bằng cách sử dụng S3 remote backend và khóa trạng thái DynamoDB để cho phép làm việc nhóm an toàn.

- Tham số hóa cấu hình tài nguyên để hỗ trợ triển khai mượt mà giữa các môi trường thử nghiệm (staging) và sản xuất (production).

- Thực thi các bài kiểm thử lập kế hoạch, xác thực và chạy thử (dry-run) để đánh giá sự phụ thuộc giữa các tài nguyên và ngăn ngừa sự sai lệch ngoài ý muốn.

> **Kiến thức rút ra:** Quản lý hạ tầng thông qua mã khai báo giúp đơn giản hóa khả năng tái tạo môi trường và thực thi quản lý phiên bản cho các tài nguyên đám mây.

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



