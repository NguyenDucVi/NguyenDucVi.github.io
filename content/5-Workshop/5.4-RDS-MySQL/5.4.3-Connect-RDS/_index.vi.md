---
title: "Kết nối EC2 đến RDS"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

## Mục tiêu

Kiểm tra kết nối database từ EC2 đến private RDS trước khi chạy TechBlog.

## Điều kiện trước khi thực hiện

- RDS status là **Available**.
- RDS cho phép port `3306` từ EC2 Security Group.

## Các bước thực hiện

Cài MariaDB client trên Amazon Linux 2023:

```bash
sudo dnf install -y mariadb105
```

Kết nối đến RDS:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

Chạy SQL kiểm tra:

```sql
SHOW DATABASES;
USE techblog;
SHOW TABLES;
```

## Cấu hình

| Hạng mục | Giá trị |
|---|---|
| Client | MariaDB client |
| Server | Amazon RDS for MySQL |
| Host | `<RDS_ENDPOINT>` |
| User | `admin` |
| Port | `3306` |

## Cách kiểm tra

MariaDB client có thể kết nối MySQL vì hai bên dùng protocol tương thích cho tác vụ này.

## Kết quả mong đợi

EC2 kết nối được RDS và liệt kê được database.

## Lỗi thường gặp

| Lỗi | Cách xử lý |
|---|---|
| Unknown MySQL server host | Kiểm tra từng ký tự của `<RDS_ENDPOINT>`. |
| Access denied | Nhập lại đúng password, không ghi password vào report. |
| Timeout | Kiểm tra lại Security Group và đường mạng trong VPC. |

## Ghi chú chi phí và bảo mật

Không dán RDS endpoint thật hoặc password trong screenshot.

<!-- TODO: Thêm /images/5-Workshop/5.4-RDS-MySQL/ec2-rds-connection.png. Caption: *Hình 5.4.3.1. MariaDB client kết nối từ EC2 đến RDS MySQL thành công.* -->
