---
title: "Đề xuất"
date: 2026-07-26
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## Tracker Maintenance – Hệ thống Quản lý Bảo trì Thiết bị trên AWS
### Giải pháp vận hành an toàn với Kiến trúc Cloud Multi-tier và Bảo mật nhiều lớp

### 1. Tóm tắt dự án

Tracker Maintenance là một ứng dụng đa tầng (Multi-tier) hiện đại được xây dựng nhằm quản lý hoạt động bảo trì thiết bị, triển khai trên nền tảng Amazon Web Services (AWS). Giao diện người dùng (Frontend) được phát triển bằng React, trong khi phần xử lý nghiệp vụ (Backend) được xây dựng bằng Spring Boot (Java 21), tích hợp với cơ sở dữ liệu quan hệ được lưu trữ an toàn trong hạ tầng mạng riêng biệt.

### 2. Mục tiêu

Các mục tiêu chính của dự án Tracker Maintenance tập trung vào việc tối ưu hóa quy trình quản lý và nâng cao tính bảo mật của hệ thống:

- Xây dựng hạ tầng Cloud ổn định với sự phân tách rõ ràng giữa các Public Subnet và Private Subnet.
- Triển khai máy chủ ứng dụng Spring Boot với mô hình bảo mật nhiều lớp và cơ chế kiểm soát truy cập chặt chẽ.
- Tối ưu hóa việc xử lý các tệp tin bảo trì và dữ liệu đa phương tiện thông qua Amazon S3 Object Storage.
- Thiết lập hệ thống giám sát và tập trung nhật ký (Log Aggregation) nhằm đảm bảo khả năng theo dõi và giám sát toàn diện.

### 3. Bài toán

- **Hiện trạng:** Các hệ thống quản lý truyền thống thường gặp khó khăn trong việc kiểm soát quyền truy cập, tiềm ẩn rủi ro về bảo mật dữ liệu và thường xảy ra tình trạng quá tải khi xử lý các tệp tin lớn thông qua máy chủ trung tâm.
- **Giải pháp:** Tracker Maintenance sử dụng Amazon VPC để cô lập tầng cơ sở dữ liệu. Ứng dụng Backend (Spring Boot) được triển khai an toàn trên Amazon EC2, kết hợp với Amazon S3 để lưu trữ tệp tin và Amazon CloudWatch để giám sát hệ thống.
- **Lợi ích:** Mang đến một hệ thống có tính sẵn sàng cao, được bảo vệ từ tầng mạng đến tầng ứng dụng, đồng thời cung cấp giao diện quản lý trực quan và trải nghiệm sử dụng mượt mà cho đội ngũ kỹ thuật.

### 4. Kiến trúc hệ thống

Toàn bộ hạ tầng được triển khai tại khu vực **ap-southeast-2 (Sydney)** với cấu trúc mạng được phân tách rõ ràng.

**Các công nghệ sử dụng:**

- **Frontend:** React / Tailwind CSS.
- **Backend:** Spring Boot (Java 21).
- **Cơ sở dữ liệu:** Amazon RDS (PostgreSQL).

**Các dịch vụ AWS chính:**

- **Amazon VPC:** Tạo môi trường mạng riêng, được chia thành Public Subnet (triển khai EC2) và Private Subnet (triển khai RDS).
- **Amazon EC2:** Máy chủ ảo chạy ứng dụng Spring Boot và xử lý toàn bộ nghiệp vụ của hệ thống.
- **Amazon RDS:** Cơ sở dữ liệu quan hệ lưu trữ thông tin hệ thống và dữ liệu bảo trì.
- **Amazon S3:** Dịch vụ lưu trữ đối tượng dành cho hình ảnh hệ thống và tài liệu kỹ thuật.
- **Amazon CloudWatch:** Dịch vụ giám sát tập trung, thu thập nhật ký hoạt động của ứng dụng.
- **Route 53 & ACM / Private CA:** Quản lý tên miền và chứng chỉ SSL/TLS để đảm bảo kết nối an toàn.
- **Amazon Bedrock:** Tích hợp trí tuệ nhân tạo nhằm hỗ trợ phân tích dữ liệu bảo trì.

![Kiến trúc hệ thống](/images/AWS_Architecture.png)
**Luồng dữ liệu chính:**

- **Luồng xử lý nghiệp vụ:** Người dùng gửi yêu cầu thông qua giao diện Frontend, dữ liệu được chuyển đến máy chủ Spring Boot trên Amazon EC2 và truy vấn thông tin từ cơ sở dữ liệu Amazon RDS nằm trong vùng mạng riêng.
- **Luồng quản lý tệp tin:** Máy chủ Spring Boot xử lý và tương tác trực tiếp với Amazon S3 để lưu trữ và truy xuất tệp tin thông qua quyền truy cập IAM được cấu hình an toàn.

### 5. Triển khai kỹ thuật

Nhóm phát triển phân chia các hạng mục kỹ thuật nhằm đảm bảo tiến độ thực hiện dự án:

- **Phát triển ứng dụng (Frontend & Backend):** Xây dựng giao diện người dùng bằng React và phát triển các API nghiệp vụ bằng Spring Boot.
- **Triển khai hạ tầng AWS:** Thiết kế kiến trúc mạng VPC, cấu hình Security Group và triển khai các dịch vụ Amazon RDS và Amazon EC2.
- **Bảo mật và giám sát:** Cấu hình chính sách IAM theo nguyên tắc **Least Privilege** và tích hợp CloudWatch Logs để giám sát hệ thống.

### 6. Lộ trình triển khai

Lộ trình triển khai dự án được chia thành các giai đoạn tuần tự:

- **Giai đoạn 1:** Khởi tạo mã nguồn, thiết kế cơ sở dữ liệu và xây dựng giao diện mẫu.
- **Giai đoạn 2:** Phát triển nghiệp vụ Backend bằng Spring Boot và thiết lập kết nối với cơ sở dữ liệu cục bộ.
- **Giai đoạn 3:** Triển khai hạ tầng AWS (VPC, Subnet, Security Group) và cấu hình Amazon RDS.
- **Giai đoạn 4:** Triển khai ứng dụng lên Amazon EC2, cấu hình Amazon S3, hoàn thiện hệ thống giám sát bằng CloudWatch và thực hiện kiểm thử tích hợp.

### 7. Đánh giá rủi ro

- **Rủi ro truy cập trái phép vào cơ sở dữ liệu:** Được loại bỏ nhờ thiết kế Amazon RDS nằm trong Private Subnet và không cho phép truy cập trực tiếp từ Internet.
- **Rủi ro rò rỉ thông tin xác thực:** Được giảm thiểu thông qua việc quản lý biến môi trường an toàn và tuân thủ nghiêm ngặt nguyên tắc phân quyền tối thiểu của IAM.

### 8. Kết quả mong đợi

Triển khai thành công hệ thống Tracker Maintenance có tính bảo mật cao, ổn định và hiệu năng tốt trên nền tảng AWS. Dự án thể hiện khả năng thiết kế kiến trúc Multi-tier và ứng dụng hiệu quả các dịch vụ điện toán đám mây hiện đại vào bài toán quản lý bảo trì thiết bị trong thực tế.