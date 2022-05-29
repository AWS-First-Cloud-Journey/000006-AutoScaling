---
title : "Khởi tạo Auto Scaling Group"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 6.   </b> "
---

#### Khởi tạo Auto Scaling Group

Ở phần này, chúng ta sẽ triển khai một Auto Scaling Group cho ứng dụng FCJ Management để đảm bảo ứng dụng của chúng ta sẽ được triển khai với tính sẵn sàng cao, và có khả năng tăng số lượng EC2 instance khi người dùng truy cập vào hệ thống tăng.

1. Truy cập vào **EC2**

- Chọn **Auto Scaling Groups**
- Chọn **Create Auto Scaling group**


![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0001-createasg.png?featherlight=false&width=90pc)

2. **Auto Scaling Group name**, nhập **```FCJ-Management-ASG```**


![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0002-createasg.png?featherlight=false&width=90pc)

3. Cấu hình template

- **Launch template**. chọn **FCJ-Management-template**
- Chọn **Next** 

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0003-createasg.png?featherlight=false&width=90pc)

4. Tiến hành cấu hình **Network**

- **VPC**, chọn **asg-vpc**
- Chọn **AZ và subnet**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0004-createasg.png?featherlight=false&width=90pc)

5. Chọn **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0005-createasg.png?featherlight=false&width=90pc)

6. Thực hiện cấu hình **Load balancing**

- Chọn **Attach to an existing load balancer**
- Chọn **Choose from your load balancer target groups**
- Chọn **FCJ-Management-TG**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0006-createasg.png?featherlight=false&width=90pc)

7. Chọn **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0007-createasg.png?featherlight=false&width=90pc)

8. Thực hiện cấu hình group size vè scaling policy.

- Desired capacity: Nhập 1. (Default)
- Minimum capacity: Nhập 1. (Default)
- Maximum capacity: Nhập 3.

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0008-createasg.png?featherlight=false&width=90pc)

9. Tại mục **Scaling policies** - optional: Lựa chọn trong bài thực hành này nhằm tạo điều kiện dễ dàng hơn cho bước kiểm tra được thực hiện tiếp theo. Bạn hoàn toàn có thể thiết lập chính sách scale tài nguyên theo nhu cầu của bạn.

- Chọn **Taget tracking scaling policy**
- **Scaling policy name**, nhập **```Target Tracking Policy```**
- **Metric type**, chọn **Application Load Balancer request count per target**.
- **Target group**, nhập **```FCJ-Management```**
- **Target value**, nhập 30

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0009-createasg.png?featherlight=false&width=90pc)

10. Chọn **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00010-createasg.png?featherlight=false&width=90pc)

11. Chọn **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00011-createasg.png?featherlight=false&width=90pc)

12. Chọn **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00012-createasg.png?featherlight=false&width=90pc)

13. Chọn **Create Auto Scaling group**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00013-createasg.png?featherlight=false&width=90pc)

14. Hòan thành tạo **Auto Scaling groups**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00014-createasg.png?featherlight=false&width=90pc)

15. Quá trình khởi tạo Auto Scaling Group sẽ được thực hiện, Auto Scaling Group vừa được tạo sẽ hiển thị trong danh sách, và bạn có thể chọn vào nó để xem thông tin chi tiết.

- Chúng ta có thể theo dõi các EC2 instance hiện có trong Auto Scaling Group ở trang **Instance management**. Các instance có tình trạng InService là các instance đã sẵn sàng hoạt động.

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00015-createasg.png?featherlight=false&width=90pc)



