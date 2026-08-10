---
title: "Tuần 1 - Nền tảng Kiến trúc Đám mây AWS, SDLC Hỗ trợ bởi AI và Bảo mật IAM"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---



### Tổng quan Tuần 1:

Trong tuần này, tôi tập trung vào ba chủ đề chính: nền tảng hạ tầng AWS, các phương pháp phát triển phần mềm hiện đại với GenAI/SDLC và những kiến thức cơ bản về bảo mật thông qua AWS Identity and Access Management (IAM).

| Lĩnh vực | Nội dung chính | Kiến thức rút ra |
| --- | --- | --- |
| A | Nền tảng Hạ tầng Toàn cầu của AWS | Hệ thống có tính sẵn sàng cao nên được thiết kế với khả năng cô lập lỗi, lý tưởng nhất là triển khai trên ít nhất hai Availability Zone (AZ). |
| B | GenAI nâng cao và Quy trình phát triển phần mềm hiện đại (SDLC) | Việc phát triển phần mềm với AI sẽ đáng tin cậy hơn khi prompt được xây dựng dựa trên cấu trúc rõ ràng, có checkpoint và được kiểm thử tự động. |
| C | Quản lý Danh tính và Quyền truy cập (IAM)  | Nguyên tắc phân quyền tối thiểu (Least Privilege) và sử dụng IAM Role tạm thời là lựa chọn an toàn nhất khi quản lý quyền trên AWS. |

### Lĩnh vực A: Nền tảng Hạ tầng Toàn cầu của AWS

Tìm hiểu các ranh giới vật lý và logic trong kiến trúc hạ tầng đám mây nhằm hỗ trợ thiết kế hệ thống có tính sẵn sàng cao (High Availability).

#### *Thứ Hai, 22/06 | Khái niệm và Lợi ích của Điện toán Đám mây*

- Tìm hiểu khái niệm điện toán đám mây là mô hình cung cấp tài nguyên CNTT theo yêu cầu thông qua Internet với hình thức thanh toán theo mức sử dụng (pay-as-you-go).
- Xác định bốn lợi ích cốt lõi của điện toán đám mây: 
  - Tối ưu chi phí
  - Tăng tốc quá trình phát triển nhờ tự động hóa và AI
  - Linh hoạt trong việc mở rộng và triển khai tài nguyên
  - Khả năng triển khai trên phạm vi toàn cầu
- Tài liệu tham khảo:

#### *Thứ Ba, 23/06 | Phân tích Cấu trúc Hạ tầng AWS*

- Nghiên cứu các thành phần trong hạ tầng AWS bao gồm:
  - **Data Centers (Trung tâm dữ liệu)**
  - **Availability Zones (AZ)**
  - **Regions**
  - **Edge Locations**
- Tìm hiểu rằng mỗi Availability Zone được cô lập về mặt lỗi nhưng vẫn kết nối với nhau thông qua mạng riêng tốc độ cao.
- Hiểu rằng mỗi Region bao gồm tối thiểu ba Availability Zone, trong khi Edge Location đóng vai trò là Point of Presence (PoP) phục vụ cho các dịch vụ như CloudFront CDN, AWS WAF và Route 53.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Một môi trường triển khai thực tế có tính sẵn sàng cao nên được thiết kế trên ít nhất hai Availability Zone nhằm đảm bảo khả năng cô lập lỗi và duy trì hoạt động của hệ thống.

### Lĩnh vực B: GenAI Nâng cao và Quy trình Phát triển Phần mềm Hiện đại

#### *Thứ Tư, 24/06 | Agentic AI và Framework của Kiro IDE*

- Tìm hiểu sự phát triển của quy trình phát triển phần mềm (SDLC), từ việc AI chỉ hỗ trợ sinh mã nguồn sang khả năng thực hiện toàn bộ quá trình phát triển tính năng.
- Nghiên cứu cách Kiro IDE/CLI chuyển đổi một prompt thành:
  - Tài liệu yêu cầu (Requirements).
  - Kiến trúc hệ thống (Architecture).
  - Timeline Checkpointing để tạo các điểm lưu an toàn và hỗ trợ quay lại phiên bản trước khi cần.
- Tài liệu tham khảo:

#### *Thứ Năm, 25/06 | Quản lý Ngữ cảnh Nâng cao và Property-Based Testing (PBT)*

- Phân tích phương pháp **Advanced Context Management** thông qua **Model Context Protocol (MCP)** để kết nối nhiều nguồn dữ liệu như:
  - Tài liệu.
  - Cơ sở dữ liệu.
  - API.
  - Thiết kế giao diện người dùng (UI).
- Tìm hiểu **Property-Based Testing (PBT)**, phương pháp tự động sinh ra nhiều bộ dữ liệu kiểm thử ngẫu nhiên dựa trên các yêu cầu được mô tả theo chuẩn **EARS**, thay vì phải viết từng test case thủ công.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Để phát triển phần mềm với AI một cách hiệu quả, cần có tài liệu đặc tả rõ ràng, quản lý ngữ cảnh đầy đủ và các cơ chế kiểm thử tự động nhằm đảm bảo chất lượng sản phẩm.

### Lĩnh vực C: Quản lý Danh tính và Quyền truy cập (AWS IAM)

#### *Thứ Sáu, 26/06 | Cấu trúc Xác thực và Phân quyền*

- Tìm hiểu các thành phần cốt lõi của AWS IAM, bao gồm: **Root User, IAM Users, Groups, JSON Policies** và **IAM Roles**.
- Tìm hiểu rằng **Root User** cần được bảo vệ bằng **Multi-Factor Authentication (MFA)** và không nên sử dụng cho các hoạt động hằng ngày.
- Hiểu vai trò của từng thành phần trong IAM:
  - **IAM Users** cung cấp thông tin xác thực dài hạn cho người dùng.
  - **Groups** hỗ trợ quản lý người dùng theo mô hình phân quyền dựa trên vai trò (Role-Based Access Control - RBAC).
  - **Policies** xác định các quyền mà người dùng hoặc dịch vụ được phép thực hiện.
  - **IAM Roles** cung cấp thông tin xác thực tạm thời để các dịch vụ AWS hoặc các tài nguyên khác có thể truy cập lẫn nhau một cách an toàn.
- Tài liệu tham khảo:
> **Kiến thức rút ra:** Cần áp dụng nguyên tắc **Least Privilege (Phân quyền tối thiểu)** và ưu tiên sử dụng IAM Roles với thông tin xác thực tạm thời khi các dịch vụ AWS cần truy cập lẫn nhau.

#### *Thứ Bảy, 27/06 | Tổng hợp và Ôn tập Kiến thức*

- Tổng hợp lại các ghi chú kỹ thuật của Tuần 1 và hệ thống hóa những kiến thức chính về kiến trúc AWS, Agentic AI và AWS IAM.
- Rà soát lại các khái niệm đã học nhằm củng cố kiến thức và chuẩn bị cho các nội dung ở những tuần tiếp theo.
- Tài liệu tham khảo:

### Kết quả đạt được

- Xây dựng được nền tảng kiến thức có hệ thống về hạ tầng cốt lõi của AWS, quy trình phát triển phần mềm hiện đại với Agentic AI (Kiro IDE) và cơ chế bảo mật của AWS IAM.
- Hiểu được cách thiết kế hệ thống có khả năng chịu lỗi dựa trên kiến trúc **Availability Zones** và **Regions** của AWS.
- Nắm được vai trò của **Model Context Protocol (MCP), Property-Based Testing (PBT)** và **Timeline Checkpointing** trong việc nâng cao chất lượng quy trình phát triển phần mềm có sự hỗ trợ của AI.
- Nắm được vai trò của Model Context Protocol (MCP), Property-Based Testing (PBT) và Timeline Checkpointing trong việc nâng cao chất lượng quy trình phát triển phần mềm có sự hỗ trợ của AI.
- Hiểu và vận dụng các nguyên tắc bảo mật của AWS IAM, đặc biệt là **Least Privilege**, sử dụng **MFA** cho Root User và ưu tiên **IAM Roles** để quản lý quyền truy cập giữa các dịch vụ.
- Hoàn thiện nền tảng kiến thức về AWS Cloud và các phương pháp phát triển phần mềm hiện đại, làm cơ sở cho việc học và triển khai dự án Data Engineering trong các tuần tiếp theo.