---
title : "Khó khăn & Hướng phát triển"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---
### Khó khăn và hướng phát triển

### Khó khăn gặp phải

* **Cấu hình bảo mật mạng và phân quyền nội bộ (Security Groups & IAM):** Trong quá trình thiết lập kết nối bảo mật giữa máy chủ ứng dụng Spring Boot (đặt trong Public Subnet) và cơ sở dữ liệu Amazon RDS (đặt trong Private Subnet), nhóm gặp khó khăn do cấu hình **Inbound Rules** của Security Group chưa chính xác, dẫn đến việc kết nối bị từ chối. Thông qua việc theo dõi nhật ký trên Amazon CloudWatch, nhóm đã xác định nguyên nhân và điều chỉnh cổng kết nối cũng như nguồn truy cập phù hợp.

* **Xung đột chính sách bảo mật lưu trữ (Bucket Policy & IAM Roles):** Khi cấu hình bảo mật cho Bucket `tracker-maintenance-images-123`, việc áp dụng chính sách **Public Access Block** quá chặt đã khiến máy chủ Backend phát sinh lỗi **Access Denied** khi ghi dữ liệu lên Amazon S3. Nhóm đã rà soát lại IAM Role và điều chỉnh chính sách phân quyền nhằm tuân thủ nguyên tắc **Principle of Least Privilege** nhưng vẫn đảm bảo hệ thống hoạt động ổn định.

* **Tính nhất quán của dữ liệu và kiểm tra đầu vào:** Dữ liệu gửi từ các yêu cầu tải tệp và thông tin bảo trì đôi khi thiếu tham số hoặc sai cấu trúc do ảnh hưởng của quá trình truyền dữ liệu, gây ra các ngoại lệ trong tầng xử lý nghiệp vụ của Spring Boot. Nhóm đã khắc phục bằng cách áp dụng cơ chế kiểm tra dữ liệu đầu vào (`@Valid`, Bean Validation) kết hợp với **Global Exception Handler** để xử lý lỗi tập trung.

### Hướng phát triển

* **Triển khai hạ tầng dưới dạng mã nguồn (Infrastructure as Code - IaC):** Chuyển toàn bộ quá trình cấu hình thủ công trên AWS Management Console (VPC, Subnets, EC2, RDS, S3, IAM) sang quản lý bằng **Terraform** hoặc **AWS CloudFormation** nhằm chuẩn hóa môi trường triển khai, dễ dàng tái tạo hạ tầng và quản lý phiên bản.

* **Tích hợp trí tuệ nhân tạo nâng cao (Amazon Bedrock):** Mở rộng khả năng phân tích thông minh bằng cách sử dụng các Foundation Models trên Amazon Bedrock để hỗ trợ chẩn đoán lỗi thiết bị dựa trên lịch sử bảo trì và đề xuất phương án xử lý phù hợp cho kỹ thuật viên.

* **Xây dựng bảng điều khiển giám sát tập trung (Fleet Dashboard):** Đồng bộ dữ liệu nhật ký từ Amazon CloudWatch và cơ sở dữ liệu lên một giao diện quản trị tập trung, cung cấp biểu đồ hiệu năng, trạng thái hoạt động của hệ thống và thông tin bảo trì theo thời gian thực, hỗ trợ công tác vận hành và giám sát hiệu quả hơn.