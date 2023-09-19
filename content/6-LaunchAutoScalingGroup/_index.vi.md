---
title : "Khởi tạo Auto Scaling Group"
date :  "`r Sys.Date()`" 
weight : 6
chapter : false
pre : " <b> 6.   </b> "
---

#### Khởi tạo Auto Scaling Group

Trong phần này, chúng ta sẽ thực hiện triển khai một Auto Scaling Group cho ứng dụng FCJ Management. Điều này đảm bảo rằng ứng dụng của chúng ta sẽ luôn sẵn sàng với tính độ tin cậy cao và khả năng tăng số lượng EC2 instance khi có nhu cầu.

1. Truy cập vào **EC2**:
   - Chọn **Auto Scaling Groups**
   - Chọn **Create Auto Scaling group**

![Auto Scaling Group](/images/16/0001.png?featherlight=false&width=90pc)

2. Nhập tên cho **Auto Scaling Group**: **```FCJ-Management-ASG```**

![Auto Scaling Group](/images/16/0002.png?featherlight=false&width=90pc)

3. Cấu hình template:
   - Chọn **Launch template** và chọn **FCJ-Management-template**
   - Chọn **Next**

![Auto Scaling Group](/images/16/0003.png?featherlight=false&width=90pc)

4. Cấu hình **Network**:
   - Chọn **VPC** đã tạo
   - Chọn **AZ và subnet**

![Auto Scaling Group](/images/16/0004.png?featherlight=false&width=90pc)

5. Chọn **Next**

![Auto Scaling Group](/images/16/0005.png?featherlight=false&width=90pc)

6. Cấu hình **Load balancing**:
   - Chọn **Attach to an existing load balancer**
   - Chọn **Choose from your load balancer target groups**
   - Chọn **FCJ-Management-TG**

![Auto Scaling Group](/images/16/0006.png?featherlight=false&width=90pc)

7. Chọn **Next**

![Auto Scaling Group](/images/16/0007.png?featherlight=false&width=90pc)

8. Cấu hình kích thước nhóm và chính sách scaling:
   - Desired capacity: Nhập 1 (Mặc định)
   - Minimum capacity: Nhập 1 (Mặc định)
   - Maximum capacity: Nhập 3

![Auto Scaling Group](/images/16/0008.png?featherlight=false&width=90pc)

9. Tại mục **Scaling policies** - tùy chọn: Trong bài thực hành này, chọn **Target tracking scaling policy** để đơn giản hóa cho bước kiểm tra tiếp theo. Bạn có thể thiết lập chính sách scale tài nguyên theo nhu cầu của bạn.
   - **Scaling policy name**: **```Target Tracking Policy```**
   - **Metric type**: Chọn **Application Load Balancer request count per target**
   - **Target group**: Chọn **FCJ-Management-TG**
   - **Target value**: Nhập 30

![Auto Scaling Group](/images/16/0009.png?featherlight=false&width=90pc)

10. Chọn **Next**

![Auto Scaling Group](/images/16/00010.png?featherlight=false&width=90pc)

11. Chọn **Create a topic**

![Auto Scaling Group](/images/16/00011.png?featherlight=false&width=90pc)

12. Cấu hình **Add notifications** và chọn **Next**

![Auto Scaling Group](/images/16/00012.png?featherlight=false&width=90pc)

- Kiểm tra email và thực hiện **Confirm subscription**

![Auto Scaling Group](/images/17/00011.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/00012.png?featherlight=false&width=90pc)

13. Chọn **Create Auto Scaling group**

![Auto Scaling Group](/images/16/00013.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00014.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00015.png?featherlight=false&width=90pc)

14. Hoàn thành việc tạo **Auto Scaling groups**

![Auto Scaling Group](/images/16/00016.png?featherlight=false&width=90pc)

15. Quá trình khởi tạo Auto Scaling Group sẽ được thực hiện. Auto Scaling Group vừa tạo sẽ hiển thị trong danh sách, bạn có thể chọn để xem thông tin chi tiết.
   - Để theo dõi các EC2 instance hiện có trong Auto Scaling Group, truy cập trang **Instance management**. Các instance có trạng thái **InService** là các instance đã sẵn sàng hoạt động.

![Auto Scaling Group](/images/16/00017.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00018.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00019.png?featherlight=false&width=90pc)
