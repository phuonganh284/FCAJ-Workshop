---
title : "Điều kiện tiên quyết"
date : 2026-07-26
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

### Điều kiện tiên quyết

### Tài khoản AWS và quyền truy cập (AWS IAM & AWS CLI)

Hệ thống yêu cầu một tài khoản AWS đang hoạt động. Để tuân thủ **nguyên tắc phân quyền tối thiểu (Principle of Least Privilege)**, dự án sử dụng **IAM User** thay vì tài khoản **Root** trong quá trình phát triển và quản trị hằng ngày. IAM User cũng được sử dụng để tạo thông tin xác thực phục vụ việc kết nối tới AWS thông qua AWS CLI.

#### Bước 1: Tạo Access Key

Đăng nhập vào **AWS Management Console** bằng tài khoản IAM và truy cập:

**IAM → Users → Security credentials**

Trong phần **Access keys**, chọn **Create access key**, lựa chọn **Command Line Interface (CLI)** làm mục đích sử dụng, xác nhận các khuyến nghị và hoàn tất quá trình tạo.

AWS sẽ sinh ra:

- **Access Key ID**
- **Secret Access Key**

Tải xuống tệp **.csv** chứa các thông tin này và lưu trữ ở nơi an toàn.

<div style="text-align: center; margin: 20px 0;">

<img src="/FCAJ-Workshop/images/iam.png" alt="iam" width="1000" />

<div style="font-weight: bold; margin-top: 8px; color: #555;">Hình 2. Trang Security credentials của IAM User trong AWS IAM.</div>

</div>

#### Bước 2: Cấu hình AWS CLI

Mở **Terminal** (Linux/macOS) hoặc **PowerShell** (Windows) và chạy lệnh:

```bash
aws configure
```

Sau đó nhập các thông tin sau:

- **AWS Access Key ID**
- **AWS Secret Access Key**
- **Default region name:** `ap-southeast-2`
- **Default output format:** `json`

Các tệp cấu hình sẽ được lưu tự động tại:

- **Linux/macOS:** `~/.aws/`
- **Windows:** `%USERPROFILE%\.aws\`

> **Lưu ý:** Mục **IAM → Security credentials → Access keys** được sử dụng để tạo thông tin xác thực cho AWS CLI.

---

### Môi trường phát triển cục bộ

Để phát triển, biên dịch và triển khai ứng dụng Spring Boot, máy tính cần cài đặt các phần mềm sau:

- **Java Development Kit (JDK) 21** để phát triển ứng dụng.
- **Maven hoặc Gradle** để quản lý thư viện và biên dịch dự án.
- **Git** để quản lý mã nguồn và theo dõi phiên bản.

Ngoài ra, cần chuẩn bị các biến môi trường nhằm lưu trữ an toàn các thông tin cấu hình quan trọng như:

- Thông tin kết nối cơ sở dữ liệu.
- Cấu hình Amazon S3.
- Cấu hình Amazon CloudWatch.

Các tệp cấu hình chứa thông tin nhạy cảm không nên được đưa lên kho mã nguồn. Cần cấu hình tệp `.gitignore` phù hợp trước khi đẩy mã nguồn lên Git.

---

### Khu vực triển khai AWS

Theo kiến trúc của dự án, toàn bộ tài nguyên AWS được triển khai tại khu vực:

```text
ap-southeast-2 (Asia Pacific – Sydney)
```

Việc sử dụng thống nhất một AWS Region giúp các dịch vụ như **Amazon VPC**, **Amazon EC2**, **Amazon RDS**, **Amazon S3** và **Amazon CloudWatch** có thể giao tiếp hiệu quả, giảm độ trễ và tránh các lỗi triển khai do tài nguyên nằm ở nhiều Region khác nhau.