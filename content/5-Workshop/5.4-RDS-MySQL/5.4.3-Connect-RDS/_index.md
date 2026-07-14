---
title: "Connect from EC2 to RDS"
date: 2026-07-10
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

## Objective

Verify database connectivity from EC2 to private RDS before running TechBlog.

## Prerequisites

- RDS status is **Available**.
- RDS allows port `3306` from the EC2 security group.

## Steps

Install the MariaDB client on Amazon Linux 2023:

```bash
sudo dnf install -y mariadb105
```

Connect to RDS:

```bash
mysql -h <RDS_ENDPOINT> -P 3306 -u admin -p
```

Run verification SQL:

```sql
SHOW DATABASES;
USE techblog;
SHOW TABLES;
```

## Configuration

| Item | Value |
|---|---|
| Client | MariaDB client |
| Server | Amazon RDS for MySQL |
| Host | `<RDS_ENDPOINT>` |
| User | `admin` |
| Port | `3306` |

## Verification

The MariaDB client can connect to MySQL because both use compatible client/server protocol for this task.

## Expected Result

EC2 can connect to RDS and list databases.

## Common Issues

| Issue | Fix |
|---|---|
| Unknown MySQL server host | Check each character of `<RDS_ENDPOINT>`. |
| Access denied | Re-enter the correct password without writing it in the report. |
| Timeout | Re-check security group and VPC path. |

## Cost and Security Notes

Do not paste the real RDS endpoint or password in screenshots.

<!-- TODO: Add /images/5-Workshop/5.4-RDS-MySQL/ec2-rds-connection.png. Caption: *Figure 5.4.3.1. Successful MariaDB client connection from EC2 to RDS MySQL.* -->
