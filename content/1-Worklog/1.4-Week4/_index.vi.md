---
title: "Tuần 4 - Thiết kế và Triển khai Pipeline Thu thập Dữ liệu cho Financial Data Lake"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---



### Tổng quan Tuần 4:

Trong Tuần 4, tôi tập trung vào việc thiết kế và triển khai pipeline thu thập dữ liệu cốt lõi cho dự án **Financial Data Lake**. Tuần làm việc bắt đầu bằng việc đánh giá các kiến trúc Cloud khác nhau để lựa chọn mô hình phù hợp. Dựa trên kiến trúc đã chọn, tôi tiếp tục xây dựng quy trình thu thập dữ liệu ban đầu, bao gồm kiểm tra nhà cung cấp dữ liệu, phát triển Provider Adapter, xử lý theo lô (batch processing) và đánh giá khả năng mở rộng của hệ thống trong quá trình thu thập dữ liệu chứng khoán Việt Nam.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Đánh giá Kiến trúc và Thiết kế Pipeline | Việc so sánh các kiến trúc Cloud khác nhau giúp lựa chọn được giải pháp có khả năng mở rộng, tối ưu chi phí và dễ bảo trì cho hệ thống thu thập dữ liệu tài chính. |
| B | Triển khai Pipeline Thu thập Dữ liệu | Xây dựng các Provider Adapter và Ingestion Worker có khả năng tái sử dụng là nền tảng để tự động hóa quá trình thu thập dữ liệu một cách ổn định. |
| C | Xử lý Batch và Đánh giá Khả năng Mở rộng | Áp dụng cơ chế retry, checkpoint và xử lý theo lô giúp tăng tính ổn định của pipeline và chuẩn bị cho việc mở rộng hệ thống trong tương lai. |

### Lĩnh vực A: Đánh giá Kiến trúc và Thiết kế Pipeline

#### *Thứ Hai, 13/07 | Đánh giá Kiến trúc Financial Data Lake*
- Tìm hiểu các mô hình kiến trúc khác nhau để xây dựng **Financial Data Lake**, bao gồm kiến trúc triển khai bằng container truyền thống và kiến trúc serverless theo hướng event-driven.
- So sánh giữa giải pháp sử dụng **Amazon RDS** và **Amazon S3** về độ phức tạp khi triển khai, khả năng mở rộng, chi phí vận hành và khả năng bảo trì.
- Nghiên cứu kiến trúc **AWS Serverless Financial Data Lake**, bao gồm các dịch vụ:
  - Amazon EventBridge
  - AWS Lambda
  - Amazon SQS
  - Amazon S3
  - AWS Glue Catalog
  - Amazon Athena
  - Amazon API Gateway
- Phân tích vai trò của từng dịch vụ trong quá trình thu thập, xử lý, lưu trữ và phân tích dữ liệu.
- Tài liệu tham khảo: Architecture Comparison Document

> **Kiến thức rút ra:** Kiến trúc serverless giúp giảm đáng kể độ phức tạp trong vận hành, đồng thời hỗ trợ khả năng mở rộng tự động và tối ưu chi phí cho các bài toán thu thập dữ liệu tài chính theo định kỳ.

#### *Thứ Ba, 14/07 | Thiết kế Pipeline Thu thập Dữ liệu trên Môi trường Cục bộ*
- Thiết kế tổng thể quy trình thu thập dữ liệu trước khi triển khai lên môi trường Cloud.
- Xác định vai trò và trách nhiệm của các thành phần trong pipeline, bao gồm:
  - Universe Loader
  - Provider Adapter
  - Dispatcher
  - Worker
  - Validator
- Hoàn thiện danh sách ban đầu của các công ty niêm yết (Initial Universe) và kiểm tra khả năng cung cấp dữ liệu thông qua các bài kiểm thử (Provider Smoke Test).
- Thiết kế cấu trúc lưu trữ dữ liệu thô (Bronze Layer) trên môi trường cục bộ để lưu các phản hồi dạng JSON trước khi thực hiện các bước ETL.
- Tài liệu tham khảo: Implementation Guide Draft
> **Kiến thức rút ra:** Việc tách biệt lớp Provider, Worker và Validator giúp pipeline có tính mô-đun cao hơn, đồng thời tạo điều kiện thuận lợi cho việc chuyển từ môi trường cục bộ sang các dịch vụ AWS trong tương lai.

### Lĩnh vực B: Triển khai Pipeline Thu thập Dữ liệu

#### *Thứ Tư, 15/07 | Phát triển Provider Adapter và Ingestion Worker*
- Xây dựng **Provider Adapter** để thu thập dữ liệu OHLCV từ nguồn dữ liệu tài chính đã lựa chọn.
- Phát triển **Ingestion Worker** có khả năng xử lý lần lượt nhiều mã cổ phiếu trong một phiên thực thi.
- Bổ sung cơ chế **Retry** và **Backoff** nhằm tăng độ ổn định khi xảy ra các lỗi tạm thời từ phía nhà cung cấp dữ liệu.
- Xây dựng cơ chế ghi log có cấu trúc, bao gồm các thông tin như:
  - Mã cổ phiếu.
  - Thời gian thực thi.
  - Trạng thái của Provider.
  - Kết quả thu thập dữ liệu.
- Tài liệu tham khảo: Implementation Guide Draft
> **Kiến thức rút ra:** Cơ chế Retry kết hợp với hệ thống Logging tập trung giúp tăng đáng kể tính ổn định của pipeline mà không làm tăng độ phức tạp trong quá trình triển khai.

#### *Thứ Năm, 16/07 | Thực thi Batch trên Môi trường Cục bộ và Kiểm tra Pipeline*
- Thực hiện thu thập dữ liệu theo lô (Batch Ingestion) đối với danh sách các mã cổ phiếu đã được lựa chọn.
- Kiểm tra mức độ đầy đủ của dữ liệu thu thập được và phân loại các yêu cầu thành công hoặc thất bại.
- Kiểm thử cơ chế **Checkpoint** để đảm bảo pipeline có thể tiếp tục từ vị trí đã dừng khi xảy ra gián đoạn mà không cần thực hiện lại toàn bộ quá trình.
- Đánh giá cấu trúc lưu trữ dữ liệu dạng **Raw JSON** trên môi trường cục bộ và chuẩn bị cho giai đoạn xử lý **Curated Data**.
- Tài liệu tham khảo: *Implementation Guide Draft*
> **Kiến thức rút ra:** Việc kết hợp xử lý theo lô với cơ chế Checkpoint giúp tăng khả năng chịu lỗi và giảm thiểu việc xử lý lại dữ liệu không cần thiết.

### Lĩnh vực C: Đánh giá Khả năng Mở rộng và Định hướng Phát triển Pipeline

#### *Thứ Sáu, 17/07 | Đánh giá Khả năng Mở rộng và Lập Kế hoạch Phát triển Pipeline*
- Đánh giá khả năng mở rộng của pipeline khi tăng số lượng mã cổ phiếu cần xử lý.
- Nghiên cứu các chiến lược xử lý đồng thời (Concurrency), giới hạn tốc độ gửi yêu cầu (Rate Limiting) và lập lịch gửi yêu cầu đến nhà cung cấp dữ liệu.
- Tìm hiểu cách tích hợp pipeline thu thập dữ liệu với các thành phần trong tương lai như:
  - ETL.
  - Feature Store.
  - Predictive Analytics.
- Đề xuất các hướng mở rộng nhằm tích hợp Machine Learning dựa trên các bộ dữ liệu tài chính đã được xử lý.
- Tài liệu tham khảo: *Predictive Analytics Proposal*
> *Kiến thức rút ra:* Thiết kế pipeline theo hướng mô-đun và có khả năng mở rộng ngay từ đầu sẽ giúp hệ thống dễ dàng tích hợp với các thành phần phân tích dữ liệu và Machine Learning trong tương lai.

### Kết quả đạt được
- Đánh giá và lựa chọn kiến trúc serverless phù hợp cho dự án **Financial Data Lake**.
- Thiết kế quy trình thu thập dữ liệu trên môi trường cục bộ và hoàn thiện danh sách ban đầu của các mã cổ phiếu.
- Xây dựng **Provider Adapter** có khả năng tái sử dụng cùng với các cơ chế **Retry**, **Logging** và **Validation** nhằm tăng tính ổn định của hệ thống.
- Xây dựng nền tảng cho quá trình thu thập dữ liệu theo lô thông qua cơ chế **Checkpoint** và **Fault Recovery**, giúp pipeline có khả năng mở rộng và chịu lỗi tốt hơn.
- Chuẩn bị pipeline cho các giai đoạn tiếp theo như xử lý ETL, Feature Engineering và tích hợp các mô hình **Predictive Analytics**.