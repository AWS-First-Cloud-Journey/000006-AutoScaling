---
title : "Tạo VPC"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

####  Tạo VPC


1. Truy cập vào [AWS Management Console](https://aws.amazon.com/premiumsupport/knowledge-center/sign-in-console/)

- Tìm **VPC**
- Chọn **VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0001-createvpc.png?featherlight=false&width=90pc)

2. Trong giao diện **VPC**

- Chọn **Your VPCs**
- Chọn **Create VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0002-createvpc.png?featherlight=false&width=90pc)

3. Trong giao diện **Create VPC**

- Chọn **VPC, subnets, etc,**
- **Name**, nhập **```asg```**
- **IPv4 CIDR block**, nhập **10.0.0.0/16**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0003-createvpc.png?featherlight=false&width=90pc)

4. Chọn **Create VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0004-createvpc.png?featherlight=false&width=90pc)

5. Tạo VPC thành công và chọn **View VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0005-createvpc.png?featherlight=false&width=90pc)

6. Thông tin chi tiết VPC vừa tạo.

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0006-createvpc.png?featherlight=false&width=90pc)

7. Thực hiện cấp phát IP public.

- Chọn **Subnets**
- Chọn **public subnet** 
- Chọn **Edit subnet settings**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0007-createvpc.png?featherlight=false&width=90pc)

8. Chọn **Enable auto-assign public IPv4 address**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0008-createvpc.png?featherlight=false&width=90pc)

9. Kiểm tra đã cấp phát thành công.

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0009-createvpc.png?featherlight=false&width=90pc)

10. Thực hiện cấp phát cho Public subnet còn lại (làm tương tự).
