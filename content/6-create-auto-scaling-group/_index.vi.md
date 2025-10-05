---
title: "Tạo Auto Scaling Group"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<strong>6. </strong>"
---

#### Vấn đề ở phần trước

**ℹ️ Information**: Ở phần kiểm thử kết quả trước đó, chúng ta nhận thấy khi ứng dụng nhận nhiều request, hiệu suất không còn ổn định. Giải pháp là tăng số lượng EC2 Instance trong hệ thống và sử dụng Load Balancer để phân phối các yêu cầu từ người dùng.

Tuy nhiên, phương pháp thủ công không hiệu quả vì để khởi tạo một EC2 Instance mới, chúng ta cần đảm bảo mỗi instance đều có đầy đủ ứng dụng, thư viện và cấu hình cần thiết để xử lý các yêu cầu.

#### Thiết lập Auto Scaling Group

#### Tạo Auto Scaling Group

Ở giao diện quản lý **EC2**, kéo bảng lựa chọn bên trái xuống cuối:

- Chọn **Auto Scaling Groups**
- Ấn **Create Auto Scaling group**

![6.1](/images/6-create-auto-scaling-group/6.1.png)

Trong giao diện tạo **Auto Scaling group**, điền các thông tin sau:

- Name: `FCJ-Management-ASG`
- Trong Launch template:
  - Launch template: chọn `FCJ-Management-template`
  - Version: **Default (1)**

![6.2](/images/6-create-auto-scaling-group/6.2.png)

**⚠️ Warning**: Tên của ASG nên đặt đúng với tên ASG đã được đặt ở phần **2.6** trước đó, để đảm bảo tính nhất quán cho Predictive Scaling.

**🔒 Security Note**: **Launch template** được chọn cho ASG phải là template đã được cài đặt đầy đủ _MySQL Client_, _Node_, _Source Code_ và _PM2_ để đảm bảo các Target hoạt động bình thường. Nếu bạn đã làm theo các bước trong phần **2** và phần **3**, bạn đã thiết lập đúng.

![6.3](/images/6-create-auto-scaling-group/6.3.png)

#### Thiết lập mạng

Trong phần Network, cấu hình như sau:

- VPC: chọn VPC **AutoScaling-Lab** đã tạo trước đó
- Availability Zones and subnets: chọn **3 public subnets** đã tạo
- Ấn **Next**

![6.4](/images/6-create-auto-scaling-group/6.4.png)

#### Thiết lập Load Balancer

**ℹ️ Information**: Trước đó chúng ta đã tạo **Application Load Balancer** và **Target Group** đã được gắn vào bộ cân bằng tải. Giờ chúng ta sẽ kết nối ASG với Load Balancer đó.

- Load balancing: chọn **Attach to an existing load balancer**
- Attach to an existing load balancer: chọn **Choose from your load balancer target group**
- Existing load balancer target group: chọn **FCJ-Management-TG | HTTP**

![6.5](/images/6-create-auto-scaling-group/6.5.png)

**💡 Pro Tip**: Khi cấu hình đúng Target Group và Application Load Balancer, lựa chọn **Existing load balancer target group** sẽ hiển thị Target Group đã tạo, xác nhận rằng cả ALB và TG đều tồn tại và được cấu hình đúng.

Trong phần VPC Lattice integration options: chọn **No VPC Lattice service** (không sử dụng trong bài lab này)

Tiếp theo, ở phần Health checks:
- Tích chọn **Turn on Elastic Load Balancing health checks**
- Giữ các thiết lập còn lại theo mặc định

![6.6](/images/6-create-auto-scaling-group/6.6.png)

#### Thiết lập Size và Scaling Policies

**ℹ️ Information**: Trong phần này, chúng ta xác định hành vi mở rộng của Group và số lượng Instance sẽ được khởi tạo trong quá trình Scale out (mở rộng) và Scale in (thu hẹp).

- Trong phần Group size:
  - Desired capacity: **1**
- Trong phần Scaling limits:
  - Min desired capacity: **1**
  - Max desired capacity: **3**

![6.7](/images/6-create-auto-scaling-group/6.7.png)

Trong phần Additional settings, ở mục Monitoring:
- Tích chọn **Enable group metrics collection within CloudWatch**
- Ấn **Next**

![6.8](/images/6-create-auto-scaling-group/6.8.png)

Trong Automatic scaling - optional: chọn **No scaling policies** (tạm thời chưa thiết lập chính sách scaling cho ASG)

![6.9](/images/6-create-auto-scaling-group/6.9.png)

Trong Instance maintenance policy: chọn **No policy**

![6.10](/images/6-create-auto-scaling-group/6.10.png)

**💡 Pro Tip**: Chúng ta không thiết lập chính sách scaling ngay lúc này vì sẽ thực hiện 4 chiến lược scaling khác nhau trong các bước tiếp theo.

#### Thiết lập thông báo

**ℹ️ Information**: Trong phần này, chúng ta thiết lập thông báo qua email (sử dụng Amazon SNS) khi ASG thực hiện các hành động như:
- Khởi tạo Instance mới
- Huỷ Instance
- Thất bại khi khởi tạo Instance
- Thất bại khi huỷ Instance

Cấu hình thông báo:
- Send a notification to: `asg-topic` (tạo topic mới)
- With these recipients: nhập email bạn muốn nhận thông báo
- Event types: chọn tất cả
- Ấn **Next**

![6.11](/images/6-create-auto-scaling-group/6.11.png)

![6.12](/images/6-create-auto-scaling-group/6.12.png)

Xác nhận lại các thông tin và ấn **Create Auto Scaling group**

![6.13](/images/6-create-auto-scaling-group/6.13.png)

#### Kết quả

**⚠️ Warning**: Trong quá trình tạo, bạn sẽ nhận được email xác nhận đăng ký từ SNS topic. Hãy kiểm tra và xác nhận đăng ký để nhận các thông báo tiếp theo.

![6.14](/images/6-create-auto-scaling-group/6.14.png)

![6.15](/images/6-create-auto-scaling-group/6.15.png)

Vì chúng ta đã thiết lập **Desired capacity = 1**, ASG sẽ tự động tạo một Instance mới, và bạn sẽ nhận được email thông báo.

![6.16](/images/6-create-auto-scaling-group/6.16.png)

Vào tab Activity của ASG FCJ-Management-ASG để kiểm tra:

![6.17](/images/6-create-auto-scaling-group/6.17.png)

**💡 Pro Tip**: Trong quá trình thực hiện các chiến lược scaling khác nhau, bạn có thể nhận được nhiều email thông báo. Đây là chủ đích khi chúng ta thiết lập SNS, giúp theo dõi và kiểm soát tốt hơn các hoạt động của Auto Scaling Group.
