---
title : "Tạo Security Group DB"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 2.3  </b> "
---


#### Tạo security group cho Database instance.


1. Chúng ta tạo Security group cho Database instance. Để đảm bảo bảo mật nên không cấu hình chung Security group của ứng dụng.

- Chọn **Security Group**
- Chọn **Create security group**

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0001-createsgdb.png?featherlight=false&width=90pc)

2. Thực hành cấu hình **security group**

- **Security Group name**, nhập **```FCJ-Mangement-DB-SG```**
- **Description**, nhập ```Security Group for DB instance```
- Chọn vpc vừa tạo

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0002-createsgdb.png?featherlight=false&width=90pc)

3. Cấu hình **Inbound rules**

- Chọn **Add rule**
- Chọn **MYSQL/Aurora** port 3306
- Sau đó chọn Soure là **FCJ-Management-SG** 
- Chọn **Create security group**

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0003-createsgdb.png?featherlight=false&width=90pc)

4. Hoàn thành tạo **Security group** cho database.

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0004-createsgdb.png?featherlight=false&width=90pc)