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

![Create VPC](/images/1/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **VPC**

   - Chọn **Your VPCs**
   - Chọn **Create VPC**

![Create VPC](/images/1/0002.png?featherlight=false&width=90pc)

3. Trong giao diện **Create VPC**

   - Chọn **VPC, subnets, etc,**
   - **Name**, nhập tên VPC của bạn.
   - **IPv4 CIDR block**, nhập **10.0.0.0/16**

![Create VPC](/images/1/0003.png?featherlight=false&width=90pc)

4. Chọn **Create VPC**

![Create VPC](/images/1/0004.png?featherlight=false&width=90pc)

5. Tạo VPC thành công và chọn **View VPC**

![Create VPC](/images/1/0005.png?featherlight=false&width=90pc)

6. Thông tin chi tiết VPC vừa tạo.

7. Thực hiện cấp phát IP public.

   - Chọn **Subnets**
   - Chọn **public subnet** 
   - Chọn **Edit subnet settings**

![Create VPC](/images/1/0006.png?featherlight=false&width=90pc)

8. Chọn **Enable auto-assign public IPv4 address**. Chọn **Save**

![Create VPC](/images/1/0007.png?featherlight=false&width=90pc)

9. Kiểm tra đã cấp phát thành công.

![Create VPC](/images/1/0008.png?featherlight=false&width=90pc)

10. Thực hiện cấp phát cho Public subnet còn lại (làm tương tự).
