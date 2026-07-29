---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---
### Dọn dẹp và thu hồi tài nguyên

Sau khi hoàn thành quá trình triển khai, kiểm thử và đánh giá hệ thống quản lý bảo trì, toàn bộ hạ tầng Cloud đã được thu hồi và dọn dẹp theo đúng quy trình nhằm tối ưu chi phí và tránh phát sinh chi phí không mong muốn trên tài khoản AWS.

* **Xóa dữ liệu và Bucket lưu trữ (Amazon S3):** Thực hiện xóa toàn bộ dữ liệu thử nghiệm, hình ảnh và tài liệu bảo trì được lưu trữ trong S3 Bucket (`tracker-maintenance-images-123`), sau đó xóa Bucket để giải phóng hoàn toàn không gian lưu trữ đối tượng.

* **Dừng máy chủ và thu hồi quyền truy cập (EC2 & IAM):** Thực hiện chấm dứt (Terminate) Amazon EC2 Instance nhằm giải phóng tài nguyên tính toán, đồng thời thu hồi và xóa IAM Role cùng các chính sách phân quyền đã được cấu hình theo nguyên tắc **Principle of Least Privilege**.

* **Xóa cơ sở dữ liệu và hạ tầng mạng (RDS & VPC):** Xóa Amazon RDS Database Instance (`tracker-maintenance-db`) để loại bỏ dữ liệu có cấu trúc, sau đó gỡ Internet Gateway, xóa các Route Table và xóa toàn bộ cấu hình **Tracker-VPC**, đưa môi trường mạng trở về trạng thái ban đầu.

* **Xóa dữ liệu giám sát (Amazon CloudWatch):** Xóa các CloudWatch Log Groups lưu trữ nhật ký hoạt động của ứng dụng Spring Boot, hoàn tất quá trình thu hồi và dọn dẹp toàn bộ hạ tầng Cloud đã triển khai.