---
title: "Khởi tạo Database Instance với RDS"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>2.3. </strong>"
---

#### Tạo Subnet group cho Database instance

Truy cập vào **AWS Management Console**

- Tìm **RDS**
- Chọn **RDS**

![Image](/images/2-preparation/2.3-rds/2.3.1.png?featherlight=false&width=90pc)

Tiếp tục:

- Chọn **Subnet groups**
- Chọn **Create DB subnet group**

![Image](/images/2-preparation/2.3-rds/2.3.2.png?featherlight=false&width=90pc)

Trong giao diện **Create DB subnet group**

- **Name**, nhập **`FCJ-Management-Subnet-Group`**
- **Description**, nhập **`Subnet Group for FCJ Management`**
- Chọn VPC đã tạo.

![Image](/images/2-preparation/2.3-rds/2.3.3.png?featherlight=false&width=90pc)

Tiến hành cấu hình **subnet**

- Chọn các AZ
- Chọn các Private subnet

![Image](/images/2-preparation/2.3-rds/2.3.4.png?featherlight=false&width=90pc)

Chọn **Create**

![Image](/images/2-preparation/2.3-rds/2.3.5.png?featherlight=false&width=90pc)

Thành công tạo **DB Subnet Group** với 2 AZ

![Image](/images/2-preparation/2.3-rds/2.3.6.png?featherlight=false&width=90pc)

![Image](/images/2-preparation/2.3-rds/2.3.7.png?featherlight=false&width=90pc)

#### Tạo Database instance

Truy cập vào **RDS AWS Management Console**

- Chọn **Databases**
- Chọn **Create database**

![Image](/images/2-preparation/2.3-rds/2.3.8.png?featherlight=false&width=90pc)

Chọn phương thức tạo **database**

- Chọn **Standard create**

![Image](/images/2-preparation/2.3-rds/2.3.9.png?featherlight=false&width=90pc)

Cấu hình **Engine** database

- Chọn **MySQL**

![Image](/images/2-preparation/2.3-rds/2.3.10.png?featherlight=false&width=90pc)

Cấu hình **Template**

- Chọn **Production**
- Chọn **Mutil-AZ DB instance**

![Image](/images/2-preparation/2.3-rds/2.3.11.png?featherlight=false&width=90pc)

Tiếp theo, thực hiện cài đặt chi tiết

- **DB instance identifier**, nhập **`fcj-management-db-instance`**
- **Master username**, nhập **`admin`**
- Chọn sang **Self managed**

![Image](/images/2-preparation/2.3-rds/2.3.12.png?featherlight=false&width=90pc)

Tiếp tục: - **Master password**, nhập tùy ý của bạn (trong bài lab, nhập **`123Vodanhphai`**) - **Confirm password**, nhập lại password 1 lần nữa.

![Image](/images/2-preparation/2.3-rds/2.3.13.png?featherlight=false&width=90pc)

Cấu hình chi tiết cho instace

- Chọn **`db.m5d.large`**
- Chọn **`General Purpose SSD (gp3)`**
- Allocated storage nhập vào **`20`**

![Image](/images/2-preparation/2.3-rds/2.3.14.png?featherlight=false&width=90pc)

Thực hiện cấu hình Connectivity cho db instance

- Chọn **Don't connect to an EC2 compute resouce**
- **VPC**, chọn **`AutoScaling-Lab`** đã tạo
- **Subnet group**, chọn subnet group đã tạo.

![Image](/images/2-preparation/2.3-rds/2.3.15.png?featherlight=false&width=90pc)

Tiếp tục:

- **VPC security group**, Chọn **Choose existing**
- **Security Group**, chọn **FCJ-Management-DB-SG** (tránh nhầm lẫn với SG của web).

![Image](/images/2-preparation/2.3-rds/2.3.16.png?featherlight=false&width=90pc)

Khởi tạo Initial Database với tên **`awsfcjuer`**, còn lại để mặc định.

![Image](/images/2-preparation/2.3-rds/2.3.17.png?featherlight=false&width=90pc)

Bấm **Create database**

![Image](/images/2-preparation/2.3-rds/2.3.18.png?featherlight=false&width=90pc)

Database instance đã được tạo thành công.

![Image](/images/2-preparation/2.3-rds/2.3.19.png?featherlight=false&width=90pc)

Chúng ta có được **Endpoint** và **Port** như dưới đây.

![Image](/images/2-preparation/2.3-rds/2.3.20.png?featherlight=false&width=90pc)
