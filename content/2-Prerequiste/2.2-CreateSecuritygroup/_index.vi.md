---
title : "Tạo Security Group"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2.2  </b> "
---

#### Tạo Security Group cho FCJ Management 

1. Chúng ta sẽ tạo Security group cho ứng dụng.

-Trong giao diện VPC, chọn **Security Group**
- Chọn **Create security group**

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0001-createsg.png?featherlight=false&width=90pc)

2. Thực hiện cấu hình Security Group

- **Security group name**, nhập **```FCJ-Management-SG```**
- **Description**, nhập **```Security Group for FCJ Management```**
- **VPC**, chọn **asg-vpc** vừa tạo.

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0002-createsg.png?featherlight=false&width=90pc)

3. Cấu hình **Inbound rules**

- Đầu tiên phải cấu hình **SSH** port 22 và **Source: MyIP** để có thể truy cập vào instance.
- Tiếp theo là **HTTP** port 80.
- **Custom TCP** port **5000** dành cho **FCJ Management**
- HTTPS port 443.

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0003-createsg.png?featherlight=false&width=90pc)

4. Kiểm tra **Outbound rules**và chọn **Create security group**

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0004-createsg.png?featherlight=false&width=90pc)

5. Hoàn thành tạo **Security Group** cho ứng dụng FCJ Management. Kiểm tra thông tin chi tiết Security Group.

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0005-createsg.png?featherlight=false&width=90pc)