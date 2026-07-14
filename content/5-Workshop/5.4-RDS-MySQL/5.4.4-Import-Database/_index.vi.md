---
title: "Export và import database TechBlog"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

## Mục tiêu

Chuyển database local `techblog` lên Amazon RDS for MySQL.

## Điều kiện trước khi thực hiện

- MySQL/Laragon local có database `techblog`.
- EC2 kết nối được RDS.

## Các bước thực hiện

Export trên Windows:

```powershell
mysqldump -u root techblog > C:\WORKING\techblog.sql
```

Upload lên EC2:

```powershell
scp -i "C:\WORKING\techblog-key.pem" "C:\WORKING\techblog.sql" ec2-user@<EC2_PUBLIC_IP>:/home/ec2-user/
```

Import vào RDS:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p techblog < /home/ec2-user/techblog.sql
```

Kiểm tra bảng:

```sql
USE techblog;
SHOW TABLES;
```

## Cấu hình

| Hạng mục | Giá trị |
|---|---|
| Source | Local MySQL `techblog` |
| Dump file | `C:\WORKING\techblog.sql` |
| Target | RDS database `techblog` |

## Cách kiểm tra

Database sau import cần có:

`categories`, `comment_reports`, `comments`, `editor_upgrade_requests`, `post_likes`, `posts`, `saved_collections`, `saved_posts`, `users`.

Sau khi kiểm thử S3 ở application level, kiểm tra image field của user/post và xác nhận field lưu `s3:avatars/<uuid>.<ext>` hoặc `s3:posts/<uuid>.<ext>`, không lưu binary ảnh hoặc presigned URL. Dùng ví dụ đã che thông tin thay cho user identifier thật.

## Kết quả mong đợi

RDS có schema và dữ liệu TechBlog cần cho demo ứng dụng.

## Lỗi thường gặp

| Lỗi | Cách xử lý |
|---|---|
| Import fail | Xác nhận target database `techblog` đã tồn tại. |
| Sai đường dẫn SQL file | Kiểm tra lại local path và nơi upload. |

## Ghi chú chi phí và bảo mật

Không đưa database password hoặc endpoint thật vào report.

<!-- TODO: Thêm /images/5-Workshop/5.4-RDS-MySQL/mysql-show-tables.png. Caption: *Hình 5.4.4.1. Chín bảng TechBlog đã import vào RDS.* -->
<!-- TODO: Thêm /images/5-Workshop/5.4-RDS-MySQL/s3-object-reference.png. Caption: *Hình 5.4.4.2. Database field đã che thông tin chứa S3 object reference.* -->
