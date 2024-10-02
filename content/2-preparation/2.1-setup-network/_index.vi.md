---
title: "Thiết lập hạ tầng mạng"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>2.1. </strong>"
---

#### Tạo VPC

Truy cập vào [AWS Management Console](https://aws.amazon.com/premiumsupport/knowledge-center/sign-in-console/)

- Tìm **VPC**
- Chọn **VPC**

![Image](/images/2-preparation/2.1-network/2.1.1.png?featherlight=false&width=90pc)

Trong giao diện **VPC**

- Chọn **Create VPC**

![Image](/images/2-preparation/2.1-network/2.1.2.png?featherlight=false&width=90pc)

Trong giao diện **Create VPC**

- Chọn **VPC and more**
- **Name**, nhập tên VPC của bạn. Trong bài lab này, ta đặt tên là **`AutoScaling-Lab`**
- **IPv4 CIDR block**, nhập **`10.0.0.0/16`**

![Image](/images/2-preparation/2.1-network/2.1.3.png?featherlight=false&width=90pc)

Chọn theo hướng dẫn

- Số lượng AZ là **3**
- Số lượng public subnet là **3**
- Số lượng private subnet là **3**
- Nat gateways chọn **None**

![Image](/images/2-preparation/2.1-network/2.1.4.png?featherlight=false&width=90pc)

Chọn theo hướng dẫn

- VPC endpoints chọn **None**
- Chọn **Create VPC**

![Image](/images/2-preparation/2.1-network/2.1.5.png?featherlight=false&width=90pc)

#### Thực hiện cấp phát IP public.

Thực hiện cấp phát IP public.

- Chọn **Subnets**
- Chọn **public subnet**
- Chọn **Edit subnet settings**

![Image](/images/2-preparation/2.1-network/2.1.6.png?featherlight=false&width=90pc)

Chọn **Enable auto-assign public IPv4 address**. Sau đó Chọn **Save**

![Image](/images/2-preparation/2.1-network/2.1.7.png?featherlight=false&width=90pc)

Kiểm tra đã cấp phát thành công.

![Image](/images/2-preparation/2.1-network/2.1.8.png?featherlight=false&width=90pc)

Thực hiện cấp phát cho Public subnet còn lại (làm tương tự).
Tiếp theo chúng ta sẽ tạo **Security group** cho ứng dụng.

- Trong giao diện VPC, chọn **Security groups**
- Chọn **Create security group**

![Image](/images/2-preparation/2.1-network/2.1.9.png?featherlight=false&width=90pc)

Thực hiện cấu hình **Security Group**

- **Security group name**, nhập **`FCJ-Management-SG`**
- **Description**, nhập **`Security Group for FCJ Management`**
- **VPC**,thì chọn VPC vừa tạo: **AutoScaling-Lab**.

![Image](/images/2-preparation/2.1-network/2.1.10.png?featherlight=false&width=90pc)

Cấu hình **Inbound rules**

- Đầu tiên phải cấu hình **SSH** port 22 và **Source: MyIP** để có thể truy cập vào instance.
- Tiếp theo là **HTTP** port 80.
- **Custom TCP** port **5000** dành cho **FCJ Management**
- HTTPS port 443.

![Image](/images/2-preparation/2.1-network/2.1.11.png?featherlight=false&width=90pc)

Kiểm tra **Outbound rules** và chọn **Create security group**

![Image](/images/2-preparation/2.1-network/2.1.12.png?featherlight=false&width=90pc)

#### Tạo Security group cho Database instance

Chúng ta tạo Security group cho Database instance. Để đảm bảo bảo mật nên không cấu hình chung Security group của ứng dụng.
Cấu hình **security group**

- **Security Group name**, nhập **`FCJ-Mangement-DB-SG`**
- **Description**, nhập **`Security Group for DB instance`**
- Chọn vpc vừa tạo

Cấu hình **Inbound rules**

- Chọn **Add rule**
- Chọn **MYSQL/Aurora** port 3306
- Sau đó chọn Soure là **FCJ-Management-SG**

![Image](/images/2-preparation/2.1-network/2.1.13.png?featherlight=false&width=90pc)

Kiểm tra lại Outbound rules và cuối cùng bấm Create security group

![Image](/images/2-preparation/2.1-network/2.1.14.png?featherlight=false&width=90pc)
