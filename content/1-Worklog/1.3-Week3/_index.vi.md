---
title: "Tuần 3 - Kiến trúc AWS Data Lake và Thiết kế Nền tảng Dữ liệu Tài chính"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
<!-- {{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}} -->


### Tổng quan Tuần 3:

Trong Tuần 3, tôi tập trung tìm hiểu kiến trúc **AWS Data Lake** và các dịch vụ hỗ trợ thông qua tài liệu AWS Building Data Lakes on AWS. Những kiến thức thu được sau đó được áp dụng để đánh giá và cải thiện kiến trúc, chiến lược thu thập dữ liệu cũng như thiết kế lưu trữ của dự án **Financial Data Lake**.

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Nền tảng AWS Data Lake | Hiểu rõ kiến trúc và các nguyên tắc thiết kế của AWS Data Lake là nền tảng để xây dựng hệ thống dữ liệu có khả năng mở rộng, tối ưu chi phí và sẵn sàng cho các tác vụ phân tích. |
| B | Thu thập dữ liệu, Lưu trữ và Quản trị dữ liệu | Việc tổ chức dữ liệu theo các vùng lưu trữ hợp lý và áp dụng chiến lược thu thập dữ liệu, quản lý metadata cũng như quản trị dữ liệu sẽ giúp nâng cao chất lượng dữ liệu, khả năng tìm kiếm và dễ dàng bảo trì trong dài hạn. |
| C | Hoàn thiện Kiến trúc Financial Data Lake | Áp dụng các nguyên tắc thiết kế của AWS Data Lake giúp xây dựng kiến trúc ETL có khả năng mở rộng, phục vụ cho phân tích dữ liệu, trực quan hóa dữ liệu và các ứng dụng Machine Learning trong tương lai. |
---
### Lĩnh vực A: Nền tảng AWS Data Lake

#### *Thứ Hai, 06/07 | Building Data Lakes on AWS – Tổng quan Kiến trúc*
- Tìm hiểu khái niệm **Data Lake** và vai trò của Data Lake trong các tổ chức hoạt động dựa trên dữ liệu.
- Nghiên cứu kiến trúc tham chiếu (Reference Architecture) của AWS để xây dựng Data Lake có khả năng mở rộng, bảo mật và dễ quản lý.
- Tìm hiểu sự khác biệt giữa **Cơ sở dữ liệu truyền thống (Traditional Database)**, **Data Warehouse** và **Data Lake** về cách lưu trữ, khả năng mở rộng và năng lực phân tích dữ liệu.
- Nghiên cứu các dịch vụ cốt lõi trong kiến trúc AWS Data Lake, bao gồm:
  - Amazon S3
  - AWS Glue
  - Amazon Athena
  - AWS Lambda
  - AWS Lake Formation
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Amazon S3 đóng vai trò là lớp lưu trữ trung tâm của AWS Data Lake, trong khi các dịch vụ xử lý và phân tích được tách biệt khỏi lớp lưu trữ, giúp hệ thống có khả năng mở rộng và tối ưu chi phí.

#### *Thứ Ba, 07/07 | Chiến lược Thu thập và Đồng bộ Dữ liệu*
- Tìm hiểu các phương pháp thu thập dữ liệu, bao gồm:
  - Batch Ingestion.
  - Streaming Ingestion.
  - Incremental Data Loading.
- Nghiên cứu cách các dịch vụ thu thập dữ liệu của AWS tích hợp với **Amazon S3** để xây dựng kho lưu trữ tập trung.
- Tìm hiểu các nguyên tắc thiết kế pipeline thu thập dữ liệu có khả năng mở rộng bằng **AWS Lambda** và **Amazon EventBridge**.
- Đánh giá các chiến lược thu thập dữ liệu phù hợp để lấy dữ liệu thị trường chứng khoán Việt Nam từ nhiều nguồn dữ liệu công khai khác nhau.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Đối với dữ liệu tài chính được cập nhật theo chu kỳ, phương pháp **Batch Ingestion** là lựa chọn đơn giản, ổn định và tối ưu chi phí hơn so với xử lý dữ liệu theo thời gian thực.
---
### Lĩnh vực B: Lưu trữ và Xử lý Dữ liệu trong Data Lake

#### *Thứ Tư, 08/07 | Tổ chức Dữ liệu trong Amazon S3*
- Tìm hiểu các phương pháp tổ chức dữ liệu trong Amazon S3 theo mô hình các vùng lưu trữ (Storage Zones).
- Nghiên cứu vai trò của các tầng:
  - Raw Layer
  - Curated Layer
  - Analytics (Feature) Layer
trong kiến trúc Data Lake hiện đại.
- Tìm hiểu các chiến lược phân vùng dữ liệu (Partitioning), tổ chức metadata, quy tắc đặt tên và quản lý vòng đời dữ liệu (Lifecycle Management) nhằm tối ưu việc lưu trữ và truy vấn dữ liệu.
- Phân tích tác động của việc tổ chức dữ liệu hợp lý đối với hiệu năng của quy trình ETL và các tác vụ phân tích dữ liệu.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Một cấu trúc lưu trữ được thiết kế hợp lý sẽ giúp nâng cao khả năng bảo trì, tối ưu hiệu năng truy vấn và dễ dàng mở rộng khi triển khai các bài toán Machine Learning hoặc phân tích dữ liệu trong tương lai.

#### *Thứ Năm, 09/07 | Xử lý Dữ liệu, Quản lý Metadata và Quản trị Dữ liệu*
- Tìm hiểu **AWS Glue** trong việc xử lý ETL, khám phá schema và quản lý Metadata Catalog.
- Tìm hiểu cách **AWS Glue** Crawlers tự động nhận diện cấu trúc dữ liệu và xây dựng kho metadata tập trung.
- Nghiên cứu **AWS Lake Formation** để quản trị dữ liệu, kiểm soát quyền truy cập và phân quyền trên nhiều tập dữ liệu khác nhau.
- Tìm hiểu các phương pháp đảm bảo chất lượng dữ liệu, tính nhất quán và quản trị dữ liệu trong toàn bộ vòng đời của Data Lake.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Quản lý metadata và xây dựng cơ chế quản trị tập trung là yếu tố quan trọng giúp dữ liệu trong Data Lake luôn dễ tìm kiếm, an toàn và có thể tái sử dụng trong các hệ thống quy mô lớn.
---
### Lĩnh vực C: Hoàn thiện Kiến trúc Dự án

#### *Thứ Sáu, 10/07 | Áp dụng Kiến trúc AWS Data Lake vào Nền tảng Dữ liệu Tài chính*
- Áp dụng các nguyên tắc thiết kế của AWS Data Lake để đánh giá và cải thiện kiến trúc của dự án Financial Data Lake.
- Rà soát quy trình ETL đã đề xuất, bao gồm:
  - Data Ingestion.
  - Raw Zone.
  - Curated Zone.
  - Feature Store.
  - Analytics.
  - Monitoring.
- Đánh giá việc lựa chọn các dịch vụ AWS cho dự án như:
  - Amazon S3.
  - AWS Lambda.
  - AWS Glue.
  - Amazon Athena.
  - Amazon CloudWatch.
  - Terraform.
- Thảo luận các hướng cải tiến kiến trúc nhằm nâng cao khả năng mở rộng, khả năng bảo trì, tối ưu chi phí và hỗ trợ tích hợp Machine Learning trong tương lai.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Việc áp dụng các nguyên tắc thiết kế của AWS ngay từ giai đoạn đầu giúp xây dựng nền tảng dữ liệu có khả năng mở rộng, dễ bảo trì và sẵn sàng phục vụ các tác vụ phân tích, trực quan hóa dữ liệu cũng như các ứng dụng AI trong tương lai.
---
### Kết quả đạt được
- Hiểu rõ kiến trúc **AWS Data Lake** và vai trò của các dịch vụ hỗ trợ trong hệ sinh thái AWS.
- Nắm được các nguyên tắc và thực tiễn tốt trong việc thu thập dữ liệu, tổ chức lưu trữ, quản lý metadata và quản trị dữ liệu trên AWS.
- Củng cố kiến thức về xây dựng quy trình ETL có khả năng mở rộng bằng **Amazon S3, AWS Lambda, AWS Glue và Amazon Athena.**
- Áp dụng các nguyên tắc thiết kế của AWS để cải thiện kiến trúc của dự án **Financial Data Lake**, tạo nền tảng vững chắc cho việc phát triển các chức năng phân tích dữ liệu, dashboard và tích hợp Machine Learning trong các giai đoạn tiếp theo.