---
title: "Tạo Load Balancer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>4.2. </strong>"
---

#### Tạo Load Balancer

Ở giao diện quản lý EC2, ở bảng chọn bên trái

- Chọn **Load Balancers**
- Nhấn vào nút **Create Load Balancer**

![4.2.1](/images/4-setup-load-balancer/4.2.1.png)

Xuất hiện bảng Compare and select load balancer type

- Ở phần Load balancer types
  - Ở phàn **Application Load Balancer**
  - Chọn **Create**

![4.2.2](/images/4-setup-load-balancer/4.2.2.png)

Chúng ta sẽ thấy xuất hiện bảng Create Application Load Balancer

- Ở phần **Basic configuration**
  - Load balancer name `FCJ-Management-LB`
  - Scheme **Internet-facing**
  - Load balancer IP address type **IPv4**

![4.2.2](/images/4-setup-load-balancer/4.2.3.png)

- Ở phần Network mapping
  - Chọn VPC **AutoScaling-Lab**
  - Chọn Subnet Public **ap-southeast-1a**, **ap-southeast-1b**, **ap-southeast-1c**. Lưu ý chọn **public subnet**

![4.2.4](/images/4-setup-load-balancer/4.2.4.png)

- Ở phần Security groups
  - Security groups **FCJ-Management-SG**
- Ở phần Listeners and routing
  - Default action **FCJ-Management-TG**

![4.2.5](/images/4-setup-load-balancer/4.2.5.png)

- Ở phần Summary, chúng ta có thể kiểm tra được các thông tin đã cấu hình cho Load Balancer
  - Nhấn vào nút **Create Balancer**

![4.2.6](/images/4-setup-load-balancer/4.2.6.png)

#### Kết quả

Sau khi tạo Load Balancer chúng ta chọn **FCJ-Management-LB** để xem thông tin

![4.2.7](/images/4-setup-load-balancer/4.2.7.png)

- Trong phần quản lý Load Balancer đã tạo
  - Chọn **Resource map - new** để xem tổng quan liên kết của Load Balancer

![4.2.8](/images/4-setup-load-balancer/4.2.8.png)
