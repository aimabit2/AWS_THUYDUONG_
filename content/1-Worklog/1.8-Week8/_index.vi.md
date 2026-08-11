---
title: "Tuần 8 - Xây dựng pipeline dữ liệu serverless và triển khai frontend tối ưu CloudFront."
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---



### Mục tiêu tuần 8:

Trong Tuần 8, tôi tập trung vào việc xây dựng đường ống xử lý dữ liệu serverless hoàn chỉnh và triển khai ứng dụng web frontend an toàn, tối ưu cho dự án Financial Data Lake. Đầu tuần, tôi bắt đầu với việc thiết kế các API backend dạng serverless bằng AWS Lambda, API Gateway và EventBridge để định tuyến sự kiện bất đồng bộ. Tiếp theo, tôi thiết lập hệ thống lưu trữ dữ liệu có khả năng mở rộng cùng năng lực truy vấn phân tích bằng Amazon S3 và Amazon Athena kết hợp tối ưu hóa phân vùng dữ liệu. Cuối cùng, tôi triển khai và phân phối ứng dụng frontend bằng AWS Amplify và Amazon CloudFront, áp dụng cơ chế bộ nhớ đệm tại viền (edge caching) và phân phối nội dung an toàn.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Kiến trúc Serverless Backend & Hướng sự kiện với Lambda, API Gateway & EventBridge | Tách biệt các dịch vụ backend bằng các luồng sự kiện giúp hệ thống đạt khả năng mở rộng cao, độ trễ thấp và xử lý dữ liệu bất đồng bộ tin cậy. |
| B | Lưu trữ Data Lake & Truy vấn phân tích Serverless với S3 & Athena | Cấu trúc phân vùng dữ liệu trên S3 và tối ưu truy vấn SQL bằng Athena giúp giảm đáng kể độ trễ truy vấn và chi phí vận hành phân tích. |
| C | Triển khai Frontend & Tối ưu phân phối tại Edge với Amplify & CloudFront | Lưu trữ tài nguyên web với Amplify kết hợp mạng phân phối CloudFront giúp tăng tốc độ truy cập ứng dụng và nâng cao bảo mật ở quy mô toàn cầu. |
---
### Lĩnh vực A: KIẾN TRÚC SERVERLESS BACKEND & HƯỚNG SỰ KIỆN VỚI LAMBDA, API GATEWAY & EVENTBRIDGE

#### *Thứ Hai, 10/08 | Thiết kế API RESTful với API Gateway & AWS Lambda*

- Thiết kế và triển khai các điểm cuối API RESTful bằng Amazon API Gateway để cung cấp các tính năng xử lý dữ liệu tài chính.

- Phát triển các hàm AWS Lambda không lưu trạng thái (stateless) bằng Python/Node.js để xử lý logic nghiệp vụ, xác thực dữ liệu và biến đổi yêu cầu.

- Cấu hình CORS, lược đồ xác thực yêu cầu và triển khai bộ xác thực tùy chỉnh (API Gateway Custom Authorizers) để đảm bảo truy cập an toàn cho client. 
- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Kết hợp API Gateway với Lambda tạo ra một lớp API backend có độ sẵn sàng cao, tự động mở rộng mà không tốn chi phí quản lý máy chủ.

#### *Thứ Ba, 11/08 | Tích hợp luồng xử lý bất đồng bộ với Amazon EventBridge*

- Cấu hình EventBridge Event Bus tùy chỉnh để giảm sự phụ thuộc giữa các microservice và xử lý việc xuất bản sự kiện bất đồng bộ.

- Tạo các quy tắc EventBridge Rules để định tuyến các sự kiện giao dịch tài chính thời gian thực trực tiếp đến các hàm Lambda xử lý mục tiêu.

- Triển khai Hàng chờ thư chết (Dead-Letter Queues - DLQ) và chính sách thử lại khi xử lý sự kiện thất bại nhằm đảm bảo độ tin cậy của dữ liệu. 

- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Kiến trúc hướng sự kiện dựa trên EventBridge cho phép tích hợp dịch vụ liền mạch và tăng khả năng chịu lỗi của hệ thống.
---
### Lĩnh vực B: Kiến trúc hướng sự kiện dựa trên EventBridge cho phép tích hợp dịch vụ liền mạch và tăng khả năng chịu lỗi của hệ thống.  

#### *Thứ Tư, 12/08 | Cấu trúc lưu trữ Data Lake & Quy tắc vòng đời S3 Lifecycle*

- Cấu trúc các S3 Bucket lưu trữ thành các vùng Data Lake riêng biệt: Bronze (dữ liệu thô), Silver (dữ liệu đã xử lý) và Gold (dữ liệu tổng hợp).

- Cấu hình S3 Bucket Policies, mã hóa dữ liệu tĩnh bằng KMS và thiết lập S3 Lifecycle Rules để chuyển nhật ký và dữ liệu cũ sang các tầng lưu trữ chi phí thấp hơn.

- Triển khai S3 Event Notifications để tự động kích hoạt các luồng phân tích dữ liệu downstream của Lambda ngay khi có tệp được tải lên.
- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Bố cục S3 nhiều tầng được cấu trúc tốt kết hợp với các quy tắc vòng đời tự động giúp tối ưu hóa cả tính tuân thủ bảo mật lẫn chi phí lưu trữ.

#### *Thứ Năm, 13/08 | Truy vấn phân tích dữ liệu tương tác Serverless với Amazon Athena*

- Thiết lập các bảng trong Glue Data Catalog và lược đồ dữ liệu tham chiếu đến các tệp Parquet đã được phân vùng trên Amazon S3.

- Thực thi các truy vấn SQL phân tích đã được tối ưu hóa bằng Amazon Athena để trích xuất các chỉ số tài chính ad-hoc và thông tin báo cáo.

- Áp dụng chuyển đổi định dạng tệp Parquet và phân vùng dữ liệu (theo năm/tháng/ngày) để giảm mạnh lượng dữ liệu cần quét mỗi truy vấn và cắt giảm chi phí. 
- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Tận dụng định dạng cột Parquet cùng kỹ thuật phân vùng của Athena mang lại tốc độ truy vấn SQL cực nhanh với chi phí thấp hơn nhiều so với cơ sở dữ liệu truyền thống.
---
### Lĩnh vực C: TRIỂN KHAI FRONTEND & TỐI ƯU PHÂN PHỐI TẠI EDGE VỚI AMPLIFY & CLOUDFRONT

#### *Thứ Sáu, 14/08 | Triển khai ứng dụng Web & Tăng tốc CDN với Amplify & CloudFront*

- Triển khai ứng dụng web dashboard bằng AWS Amplify với quy trình CI/CD tự động được liên kết trực tiếp với kho lưu trữ Git.

- Cấu hình các phân phối Amazon CloudFront phía trước S3 static hosting và các điểm cuối API Gateway để lưu bộ nhớ đệm tại các điểm biên (edge caching) toàn cầu.

- Tối ưu hóa hành vi lưu đệm của CloudFront, thêm tiêu đề phản hồi tùy chỉnh (Custom Response Headers) và tích hợp chứng chỉ SSL/TLS qua AWS Certificate Manager (ACM).

- Tài liệu tham khảo: 

> **Kiến thức rút ra:** Triển khai ứng dụng web dashboard bằng AWS Amplify với quy trình CI/CD tự động được liên kết trực tiếp với kho lưu trữ Git.

Cấu hình các phân phối Amazon CloudFront phía trước S3 static hosting và các điểm cuối API Gateway để lưu bộ nhớ đệm tại các điểm biên (edge caching) toàn cầu.

Tối ưu hóa hành vi lưu đệm của CloudFront, thêm tiêu đề phản hồi tùy chỉnh (Custom Response Headers) và tích hợp chứng chỉ SSL/TLS qua AWS Certificate Manager (ACM).
---
### Kết quả đạt được
- Xây dựng thành công lớp API serverless có khả năng mở rộng bằng Amazon API Gateway và AWS Lambda tích hợp sẵn cơ chế xác thực và phân quyền bảo mật.

- Thiết kế kiến trúc luồng tích hợp hướng sự kiện bằng Amazon EventBridge có xử lý ngoại lệ qua hàng chờ thư chết (DLQ).

- Tổ chức cấu trúc Data Lake trên S3 nhiều tầng với khả năng xử lý tự động theo sự kiện và áp dụng các quy tắc vòng đời tiết kiệm chi phí.

- Phân tích dữ liệu hiệu năng cao trên S3 bằng Amazon Athena kết hợp kỹ thuật phân vùng dữ liệu Parquet.

- Tối ưu hóa quy trình triển khai frontend bằng luồng CI/CD của AWS Amplify và tăng tốc phân phối nội dung toàn cầu nhờ mạng lưới Amazon CloudFront.


