---
title: "Tạo Target Group"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>4.1. </strong>"
---

#### Tạo Target Group

Ở phần giao diện quản lý EC2, ở bảng chọn bên phải, hãy kéo dưới dưới phần **Load Balancing**

- Chọn **Target Group**
- Chọn **Create target group**

![4.1.1](/images/4-setup-load-balancer/4.1.1.png)

Xuất hiện bảng **Specify group details**, hãy cấu hình theo như sau.

- Ở phần Basic configuration
  - Choose a target types **Instances**
  - Target group name `FCJ-Management-TG`

![4.1.2](/images/4-setup-load-balancer/4.1.2.png)

- Tiếp tục trong phần Basic configuration
  - Protocol : port **HTTP**, **5000**
  - IP address **IPv4**
  - VPC **AutoScaling-Lab**
  - Protocol version **HTTP1**

![4.1.3](/images/4-setup-load-balancer/4.1.3.png)

- Nhấn **Next**

![4.1.4](/images/4-setup-load-balancer/4.1.4.png)

Tiếp theo chúng ta tiến hành **Register target**

- Ở phần Available instance

  - Chọn targer group **FCJ-Management-TG**
  - Ports for the seleced instances **5000**
  - Chọn **Include as pending below**

![4.1.5](/images/4-setup-load-balancer/4.1.5.png)

- Ở phần Review targets
  - Ta sẽ thấy target group đã được đăng ký trước đó
  - Chọn **Create target group**

![4.1.6](/images/4-setup-load-balancer/4.1.6.png)

#### Kết quả

Chúng ta đã hoàn thành việc tạo Target Group, chọn Target Group **FCJ-Management-TG** vừa khởi tạo để xem thông tin.

![4.1.7](/images/4-setup-load-balancer/4.1.7.png)
