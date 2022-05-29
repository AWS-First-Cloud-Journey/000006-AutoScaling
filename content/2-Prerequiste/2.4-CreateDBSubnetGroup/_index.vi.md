---
title : "Tạo DB Subnet Group"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 2.4  </b> "
---

#### Tạo DB Subnet Group


1. Truy cập vào **[RDS](https://ap-southeast-1.console.aws.amazon.com/rds/home?region=ap-southeast-1)**

- Chọn **Subnet groups**
- Chọn **Create DB subnet group**

![Create SG](/images/2-Prerequiste/2.4-CreateDBSubnetGroup/0001-createdbsubnetgroup.png?featherlight=false&width=90pc)

2. Trong  giao diện **Create DB subnet group**

- **Name**, nhập **```FCJ-Management-Subnet-Group```**
- **Description**, nhập ```Subnet Group for FCJ Management```
- Chọn **asg-vpc** đã tạo.

![Create SG](/images/2-Prerequiste/2.4-CreateDBSubnetGroup/0002-createdbsubnetgroup.png?featherlight=false&width=90pc)

3. Tiến hành cấu hình **subnet**

- Chọn các AZ
- Chọn subnet
- Chọn **Create**

![Create SG](/images/2-Prerequiste/2.4-CreateDBSubnetGroup/0003-createdbsubnetgroup.png?featherlight=false&width=90pc)

4. Thành công tạo **DB Subnet Group**

![Create SG](/images/2-Prerequiste/2.4-CreateDBSubnetGroup/0005-createdbsubnetgroup.png?featherlight=false&width=90pc)