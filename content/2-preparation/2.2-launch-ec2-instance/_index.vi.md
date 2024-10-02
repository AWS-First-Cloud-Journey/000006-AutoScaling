---
title: "Khởi tạo EC2 Instance"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>2.2. </strong>"
---

Truy cập vào [AWS Management Console](https://aws.amazon.com/console/):

- Tìm **EC2**
- Chọn **EC2**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.1.png?featherlight=false&width=90pc)

Trong giao diện **EC2**:

- Chọn **Launch instances**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.2.png?featherlight=false&width=90pc)

Đặt tên cho instance, nhập **`FCJ-Management`**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.3.png?featherlight=false&width=90pc)

Thực hiện chọn **AMI**:

- Chọn **Quick Start**
- Chọn **Amazon Linux**
- Chọn **Amazon Linux 2023 AMI**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.4.png?featherlight=false&width=90pc)

Chọn **Instance type**:

- Chọn **t2.micro**
- Chọn **Create new key pair**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.5.png?featherlight=false&width=90pc)

Cấu hình key pair

- Đặt tên là **`fcj-key`**
- Key pair type: **RSA**
- Private key format: **.pem**
- Bấm **Create key pair**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.6.png?featherlight=false&width=90pc)

Thực hiện cấu hình **Network**:

- Bấm vào nút Edit

- **VPC**, chọn VPC đã tạo.
- **Subnet**, chọn **Public subnet**
- Kiểm tra đã **Auto-assign public IP** chưa?. Nếu chưa, xem lại bước cấp phát public IP ở bước tạo VPC.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.7.png?featherlight=false&width=90pc)
Tiếp tục:

- Chọn **Select existing security group** rồi chọn **FCJ-Management-SG**.
- Chọn **Launch instance**.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.8.png?featherlight=false&width=90pc)

Khởi tạo instance thành công.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.9.png?featherlight=false&width=90pc)
