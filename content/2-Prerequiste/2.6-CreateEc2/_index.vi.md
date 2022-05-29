---
title : "Tạo EC2 instance"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 2.6 </b> "
---


#### Tạo EC2 instance

1. Truy cập vào [AWS Management Console](https://aws.amazon.com/console/)

- Tìm **EC2**
- Chọn **EC2**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0001-createec2.png?featherlight=false&width=90pc)

2. Trong giao diện **EC2**

- Chọn **Instances**
- Chọn **Launch instances**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0002-createec2.png?featherlight=false&width=90pc)

3. Name instance, nhập **```FCJ-Management```**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0003-createec2.png?featherlight=false&width=90pc)

4. Thực hiện cho **AMI**

- Chọn **Quick Start**

- Chọn **Amazon Linux**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0004-createec2.png?featherlight=false&width=90pc)

5. Chọn **Instance type**

- Chọn **t2.micro**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0005-createec2.png?featherlight=false&width=90pc)

6. Thực hiện cấu hình **Network**

- **VPC**, chọn **asg-vpc**
- **Subnet**, chọn **Public subnet**
- Kiểm tra đã **Auto-assign public IP** chưa?. Nếu chưa xem lại bước cấp phát public IP ở bước tạo VPC.

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0006-createec2.png?featherlight=false&width=90pc)

7. Chọn **Launch instance**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0007-createec2.png?featherlight=false&width=90pc)

8. Khởi tạo instance thành công và chọn **View all instances**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0008-createec2.png?featherlight=false&width=90pc)

9. Xem chi tiết instance và ghi chú lại **Public IPv4 address** để thực hiện kết nối ở bước sau.

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0009-createec2.png?featherlight=false&width=90pc)
