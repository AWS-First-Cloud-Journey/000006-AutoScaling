---
title : "Khởi tạo Load Balancer"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5.  </b> "
---

#### Khởi tạo Load Balancer

1. Truy cập vào **EC2**

- Chọn **Load Balancers**
- Chọn **Creare Load Balancer**


![Load Balancer](/images/5-LaunchLoadBalancer/0001-createloadbalancer.png?featherlight=false&width=90pc)

2. Phần **Load balancer types**

- Chọn **HTTP/HTTPS**
- Chọn **Create**

![Load Balancer](/images/5-LaunchLoadBalancer/0002-createloadbalancer.png?featherlight=false&width=90pc)

3. Trong giao diện **Create Application Load Balancer**

- **Load balancer name**, nhập **```FCJ-Management-LB```**
- **Scheme**, chọn **Internet-facing**
- **IP address type**, chọn **IPv4**

![Load Balancer](/images/5-LaunchLoadBalancer/0003-createloadbalancer.png?featherlight=false&width=90pc)

4. Thực hiện cấu hình **Network mapping**

- **VPC**, chọn **asg-vpc**
- **Mapping**, chọn **ap-southeast-1a** và **ap-southeast-1b**
- Chọn **subnet**

![Load Balancer](/images/5-LaunchLoadBalancer/0004-createloadbalancer.png?featherlight=false&width=90pc)

5. Cấu hình **security group**, chọn **FCJ-Management-SG**.

- Phần **Listeners and routing**, trong **Default actions** chọn **FCJ-Management-TG**

![Load Balancer](/images/5-LaunchLoadBalancer/0005-createloadbalancer.png?featherlight=false&width=90pc)

6. Kiểm tra lại và chọn **Create load balancer** 

![Load Balancer](/images/5-LaunchLoadBalancer/0006-createloadbalancer.png?featherlight=false&width=90pc)

7. Tạo **Application Load Balancer** thành công và chọn **View load balancer**

![Load Balancer](/images/5-LaunchLoadBalancer/0007-createloadbalancer.png?featherlight=false&width=90pc)

8. Trong giao diện **Load Balancer**. Quá trình tạo Load Balancer sẽ mất khoảng 5-10 phút để hoàn thành. Bạn có thể kiểm tra sự thay đổi trạng thái từ provisioning sang active ở danh sách Load Balancer.

- Chọn **FCJ-Management-LB**
- Sao chép **DNS name** của Load Balancer.

![Load Balancer](/images/5-LaunchLoadBalancer/0008-createloadbalancer.png?featherlight=false&width=90pc)

9. Truy cập bằng cách dán **DNS name** vào trình duyệt.  Tuy nhiên lúc này chúng ta chỉ có 1 máy chủ EC2 duy nhất.


![Load Balancer](/images/5-LaunchLoadBalancer/0009-createloadbalancer.png?featherlight=false&width=90pc)

Tiếp theo chúng ta sẽ tiến hành cấu hình tính năng Auto Scaling Group, giúp tự động tăng số lượng EC2 instance của chúng ta khi lượng truy cập tăng cao.





