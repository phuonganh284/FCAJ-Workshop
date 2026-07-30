---
title : "Giới thiệu"
date : 2026-07-26
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

### Triển khai hạ tầng Web trên nền tảng Cloud và thiết lập bảo mật hệ thống

<div style="text-align: center; margin: 20px 0;">

  <img src="/FCAJ-Workshop/images/AWS_Architecture.png" alt="architecture" width="1000" />

  <div style="font-weight: bold; margin-top: 8px; color: #555;">Hình 1. Kiến trúc tổng thể của hạ tầng mạng và sự tích hợp các dịch vụ AWS trong dự án Tracker Maintenance.</div>
</div>

<br>

### Tổng quan

Bài thực hành này mô tả toàn bộ quá trình xây dựng, cấu hình và kiểm thử hạ tầng Cloud cho hệ thống **Tracker Maintenance**.

Quá trình triển khai tập trung vào việc xây dựng kiến trúc Web đa tầng trên AWS tại khu vực **ap-southeast-2 (Sydney)** với cấu trúc mạng được phân tách rõ ràng và luồng xử lý dữ liệu an toàn, bao gồm:

* Thiết lập **Amazon Virtual Private Cloud (VPC)** trong một **Availability Zone**, chia thành **Public Subnet** (tiếp nhận lưu lượng truy cập từ Internet) và **Private Subnet** (cô lập và bảo vệ cơ sở dữ liệu Amazon RDS).
* Triển khai ứng dụng **Spring Boot** trên **Amazon EC2** để xử lý các nghiệp vụ của hệ thống và cung cấp các RESTful API cho giao diện người dùng.
* Kết nối máy chủ ứng dụng với **Amazon RDS (PostgreSQL)** được đặt trong Private Subnet nhằm đảm bảo việc truy cập cơ sở dữ liệu luôn an toàn và ổn định.
* Lưu trữ hình ảnh bảo trì và tài liệu kỹ thuật trên **Amazon S3**, cho phép hệ thống tải lên, quản lý và truy xuất tệp tin một cách bảo mật và hiệu quả.
* Quản lý quyền truy cập thông qua **AWS Identity and Access Management (IAM)**, đồng thời sử dụng **Amazon CloudWatch** để tập trung nhật ký hệ thống, giám sát hiệu năng và theo dõi tình trạng hoạt động của hạ tầng.

Thông qua quá trình triển khai này, hệ thống **Tracker Maintenance** cung cấp một hạ tầng Cloud an toàn, ổn định và có khả năng mở rộng, đồng thời tuân thủ các thông lệ tốt nhất của AWS về mạng, lưu trữ, giám sát và bảo mật.