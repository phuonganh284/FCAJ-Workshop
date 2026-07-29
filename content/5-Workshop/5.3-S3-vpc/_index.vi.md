---
title : "Các bước triển khai"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Các bước triển khai chi tiết

### Bước 1: Thiết lập Virtual Private Cloud và định tuyến (Amazon VPC)

Bước đầu tiên là xây dựng hạ tầng mạng nhằm tách biệt các tài nguyên công khai và tài nguyên nội bộ để tăng cường bảo mật hệ thống.

- Tạo **Amazon VPC** có tên **Tracker-VPC** tại khu vực **ap-southeast-2 (Sydney)** với dải địa chỉ IPv4 **10.0.0.0/16**.
- Chia VPC thành hai Subnet:
  - **Public Subnet:** Chứa máy chủ Amazon EC2 chạy ứng dụng Spring Boot và tiếp nhận các yêu cầu từ Internet.
  - **Private Subnet:** Chứa cơ sở dữ liệu Amazon RDS và không cho phép truy cập trực tiếp từ Internet.
- Tạo và gắn **Internet Gateway (IGW)** vào VPC.
- Cấu hình **Route Table** của Public Subnet để chuyển toàn bộ lưu lượng Internet (`0.0.0.0/0`) thông qua Internet Gateway.

<div style="text-align:center; margin:20px 0;">

![VPC Resource Map](/images/vpcs.png)

<div style="font-weight:bold; margin-top:8px; color:#555;">Hình 3. Sơ đồ tài nguyên Amazon VPC.</div>

</div>

> **Lưu ý:** Kiến trúc VPC phân tách rõ ràng Public Subnet và Private Subnet, giúp cô lập các tài nguyên quan trọng khỏi truy cập trực tiếp từ Internet.

---

### Bước 2: Triển khai cơ sở dữ liệu an toàn (Amazon RDS)

Triển khai cơ sở dữ liệu **Amazon RDS PostgreSQL** trong Private Subnet để lưu trữ dữ liệu của hệ thống.

Cấu hình **Security Group** của cơ sở dữ liệu như sau:

- Chặn toàn bộ kết nối trực tiếp từ Internet.
- Chỉ cho phép kết nối từ Security Group của máy chủ EC2.

<div style="text-align:center; margin:20px 0;">

![Amazon RDS Status](/images/rds.png)

<div style="font-weight:bold; margin-top:8px; color:#555;">Hình 4. Trạng thái của Amazon RDS.</div>

</div>

> **Lưu ý:** Amazon RDS được triển khai trong Private Subnet, giúp tăng cường bảo mật bằng cách loại bỏ hoàn toàn khả năng truy cập trực tiếp từ bên ngoài.

---

### Bước 3: Triển khai máy chủ ứng dụng và cấu hình IAM (Amazon EC2 & IAM)

Trước khi triển khai ứng dụng, tạo một **IAM Role** theo nguyên tắc **Least Privilege** để cấp quyền cho EC2 truy cập Amazon S3 và Amazon CloudWatch mà không cần sử dụng thông tin xác thực cố định.

Triển khai một máy chủ **Amazon EC2** trong Public Subnet và:

- Gắn IAM Role đã tạo.
- Cấu hình Security Group cho phép lưu lượng HTTP và HTTPS.
- Cài đặt **Java Development Kit (JDK) 21**.
- Triển khai và khởi chạy ứng dụng Spring Boot.

<div style="text-align:center; margin:20px 0;">

![Amazon EC2 Configuration](/images/ec2.png)

<div style="font-weight:bold; margin-top:8px; color:#555;">Hình 5. Cấu hình máy chủ Amazon EC2.</div>

</div>

> **Lưu ý:** Máy chủ EC2 hoạt động ổn định với địa chỉ IP công khai và truy cập an toàn đến các dịch vụ AWS thông qua IAM Role.

---

### Bước 4: Cấu hình lưu trữ tệp tin (Amazon S3)

Tạo một **Amazon S3 Bucket** để lưu trữ hình ảnh và tài liệu bảo trì do người dùng tải lên.

Ứng dụng Spring Boot thực hiện tải lên và truy xuất tệp trực tiếp từ Amazon S3 thông qua quyền IAM, giúp giảm nhu cầu lưu trữ trên máy chủ EC2.

<div style="text-align:center; margin:20px 0;">

![Amazon S3 Configuration](/images/s3.png)

<div style="font-weight:bold; margin-top:8px; color:#555;">Hình 6. Cấu hình Amazon S3 Bucket.</div>

</div>

> **Lưu ý:** Amazon S3 cung cấp khả năng lưu trữ đối tượng có tính mở rộng cao, độ bền dữ liệu lớn và giảm tải cho máy chủ ứng dụng.

---

### Bước 5: Giám sát hệ thống (Amazon CloudWatch)

Cấu hình **Amazon CloudWatch** để thu thập nhật ký hoạt động của ứng dụng Spring Boot đang chạy trên Amazon EC2.

CloudWatch hỗ trợ nhóm phát triển:

- Theo dõi nhật ký ứng dụng.
- Giám sát hiệu năng hệ thống.
- Phát hiện lỗi trong quá trình vận hành.
- Hỗ trợ phân tích và khắc phục sự cố nhanh chóng.

<div style="text-align:center; margin:20px 0;">

![CloudWatch Logs](/images/cloudwatch.png)

<div style="font-weight:bold; margin-top:8px; color:#555;">Hình 7. Giám sát nhật ký bằng Amazon CloudWatch.</div>

</div>

> **Lưu ý:** Việc tập trung nhật ký giúp tăng khả năng quan sát hệ thống và đơn giản hóa quá trình giám sát cũng như xử lý sự cố.