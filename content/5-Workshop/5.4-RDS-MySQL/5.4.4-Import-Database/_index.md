---
title: "Export and Import the TechBlog Database"
date: 2026-07-10
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

## Objective

Move the local `techblog` database to Amazon RDS for MySQL.

## Prerequisites

- Local MySQL/Laragon contains database `techblog`.
- EC2 can connect to RDS.

## Steps

Export on Windows:

```powershell
mysqldump -u root techblog > C:\WORKING\techblog.sql
```

Upload to EC2:

```powershell
scp -i "C:\WORKING\techblog-key.pem" "C:\WORKING\techblog.sql" ec2-user@<EC2_PUBLIC_IP>:/home/ec2-user/
```

Import into RDS:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p techblog < /home/ec2-user/techblog.sql
```

Check tables:

```sql
USE techblog;
SHOW TABLES;
```

## Configuration

| Item | Value |
|---|---|
| Source | Local MySQL `techblog` |
| Dump file | `C:\WORKING\techblog.sql` |
| Target | RDS database `techblog` |

## Verification

The imported database should contain:

`categories`, `comment_reports`, `comments`, `editor_upgrade_requests`, `post_likes`, `posts`, `saved_collections`, `saved_posts`, `users`.

After application S3 testing, inspect the relevant user/post image field and confirm it stores `s3:avatars/<uuid>.<ext>` or `s3:posts/<uuid>.<ext>`, rather than binary content or a presigned URL. Use a redacted example instead of a real user identifier.

## Expected Result

RDS contains the TechBlog schema and data needed for the application demo.

## Common Issues

| Issue | Fix |
|---|---|
| Import fails | Confirm target database `techblog` exists. |
| Wrong SQL file path | Re-check local path and upload destination. |

## Cost and Security Notes

Do not include database passwords or real endpoint values in the report.

<!-- TODO: Add /images/5-Workshop/5.4-RDS-MySQL/mysql-show-tables.png. Caption: *Figure 5.4.4.1. Nine TechBlog tables imported into RDS.* -->
<!-- TODO: Add /images/5-Workshop/5.4-RDS-MySQL/s3-object-reference.png. Caption: *Figure 5.4.4.2. Redacted database field containing an S3 object reference.* -->
