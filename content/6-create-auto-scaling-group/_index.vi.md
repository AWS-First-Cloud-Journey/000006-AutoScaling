---
title: "Tạo Auto Scaling Group"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<strong>6. </strong>"
---

### Vấn đề ở phần trước

Ở phần kiểm thử kết quả ở bên trên, thì chúng ta có thể thấy là khi ứng dụng có nhiều request tới thì nó sẽ hoạt động không còn ổn định nữa và giải pháp là chúng ta sẽ phải tăng thêm nhiều EC2 Instance ở trong hệ thống và nhờ vào Load Balancer để chia sẻ các yêu cầu từ phía người dùng.

Tuy nhiên tới phương pháp thủ công này thì sẽ không được hợp lý cho lắm, bởi vì để khởi tạo một EC2 Instance, thì mình cần phải có được cái "lõi" ở bên trong, chính là ứng dụng đang đảm nhận nhiệm vụ xử lý các yêu cầu đó và cùng với các thư viện khác.

### Thiết lập Auto Scaling Group

#### Thiết lập Launch template

Ở trong giao diện quản lý của **EC2**, kéo bảng lựa chọn ở bên phải xuống cuối cùng.

- Chọn **Auto Scaling Groups**.
- Ấn **Create Auto Scaling group**.

![6.1](/images/6-create-auto-scaling-group/6.1.png)

Ở trong giao diện tạo **Auto Scaling group**, chúng ta sẽ điền các thông tin sau

- Name: `FCJ-Management-ASG`
- Trong Launch template:
  - Launch template: chọn `FCJ-Management-template` (có thể là bất kỳ cái tên nào).
  - Version: **Default (1)** theo như lựa chọn mặc định.

![6.2](/images/6-create-auto-scaling-group/6.2.png)

{{% notice note %}}
Lưu ý là tên của ASG bạn nên đặt đúng với tên của ASG mà được đặt ở trong phần **2.6** trước đó, bước chuẩn bị dữ liệu cho Predictive Scaling.
{{% /notice %}}

{{% notice note %}}
**Launch template** được chọn cho ASG phải là template mà được cài đặt đầy đủ _MySQL Client_, _Node_, _Source Code_ và _PM2_ thì mới đảm bảo các Target hoạt động bình thường, nếu như bạn làm theo các bướcr trong phần **2** và phần **3** thì bạn đã làm đúng.
{{% /notice %}}

![6.3](/images/6-create-auto-scaling-group/6.3.png)

#### Thiết lập mạng

Ở trong phần Network, chọn các thông tin như sau:

- VPC: chọn VPC **AutoScaling-Lab**, VPC mà chúng ta đã tạo ở đầu bài.
- Availability Zones and subnets: chọn **3 public subnets** mà chúng ta đã tạo.
- Ấn **Next**.

![6.4](/images/6-create-auto-scaling-group/6.4.png)

#### Thiết lập Load Balancer và một số thứ khác

Ở trước đó thì chúng ta đã có tạo **Application Load Balancer** và tạo một **Target Group** và gắn vào trong bộ cân bằng tải đó. Nên giờ chúng ta sẽ chọn một số lựa chọn như sau:

- Load balancing: chọn **Attach to an existing load balancer**.
- Attach to an existing load balancer: chọn **Choose from your load balancer target group**
- Existing load balancer target group: chọn **FCJ-Management-TG | HTTP**.

![6.5](/images/6-create-auto-scaling-group/6.5.png)

{{% notice note %}}
Khi cấu hình đúng Target Group và **Application Load Balancer**, thì ở lựa chọn **Existing load balancer target group** chúng ta có thể thấy được **Target Group** đó được liệt kê, nghĩa là cả ALB và TG đều tồn tại.
{{% /notice %}}

Trong phần VPC Lattice integration options: chọn **No VPC Lattice service**, trong bài này thì chúng ta không cấu hình phần này.

Tiếp theo là Health checks, chúng ta sẽ chọn (tích) **Turn on Elastic Load Balancing health checks**. Để các thiết lập còn lại theo mặc định.

![6.6](/images/6-create-auto-scaling-group/6.6.png)

Trong phần Additional settings, ở phần Monitoring:

- Chọn (tích) **Enable group metrics collection within CloudWatch**.
- Ấn **Next**.

![6.7](/images/6-create-auto-scaling-group/6.7.png)

#### Thiết lập Size và Scaling cho Group

Ở trong phần này thì mình sẽ xác định các hành vi mở rộng của Group và số lượng các Instance sẽ được khởi tạo trong quá trình Scale, bao gồm Scale out (mở rộng) và Scale in (thu hẹp).

- Trong phần Group size:
  - Desired capacity: **1**
- Trong phần Scaling:
  - Scaling limits:
    - Min desired capacity: **1**
    - Max desired capacity: **3**

![6.8](/images/6-create-auto-scaling-group/6.8.png)

Trong Automatic scaling - optional: chọn **No scaling policies**, tạm thời làm mình sẽ không thiết lập chính sách scaling cho ASG.

![6.9](/images/6-create-auto-scaling-group/6.9.png)

Trong Instance maintenace policy: chọn **No policy**.

![6.10](/images/6-create-auto-scaling-group/6.10.png)

{{% notice note %}}
Ở đây chúng ta sẽ không thiết lập chính sách cho ASG là vì mình sẽ thực hiện các chiến lược Scaling sau, bao gồm 4 chiến lược khác nhau.
{{% /notice %}}

#### Thiết lập thông báo

Trong phần này, chúng ta sẽ thiết lập thông báo tới email (dùng Amazon SNS) khi mà ASG:

- Khởi tạo một Instance mới.
- Huỷ một Instance.
- Thất bại khi khởi tạo Instance.
- Thất bại khi huỷ một instance.

Chúng ta sẽ chỉ tạo thông báo tới một email duy nhất, bao gồm các thông tin:

- Send a notification to: `asg-topic`. Mình sẽ chọn một topic để gửi.
- With these recipents: nhập email mà bạn muốn SNS gửi tới.
- Event types: chọn tất cả.
- Ấn **Next**.

![6.11](/images/6-create-auto-scaling-group/6.11.png)

![6.12](/images/6-create-auto-scaling-group/6.12.png)

Xác nhận lại các thông tin và **Create Auto Scaling group**.

![6.13](/images/6-create-auto-scaling-group/6.13.png)

#### Kết quả

Trong quá trình tạo thì sẽ có một email gửi tới, nhớ kiểm tra và đăng ký nhận email từ topic đó.

![6.14](/images/6-create-auto-scaling-group/6.14.png)

![6.15](/images/6-create-auto-scaling-group/6.15.png)

Vì ở trên chúng ta chỉnh thông số **Desired capacity = 1**, nên khi được tạo ra thì ASG sẽ tự động tạo cho hệ thống một Instance mới, lúc này thì chúng ta sẽ nhận được email mới.

![6.16](/images/6-create-auto-scaling-group/6.16.png)

Vào trong tab Activity của ASG FCJ-Management-ASG để kiểm tra

![6.17](/images/6-create-auto-scaling-group/6.17.png)

{{% notice note %}}
Trong quá trình thực hiện các chiến lược scaling khác, bạn có thể sẽ nhận được rất nhiều email, nên hãy chú ý trong Email Box. Đây cũng là chủ đích khi chúng ta tạo SNS để thông báo, nhắm dễ kiểm soát được điều gì đang diễn ra hơn.
{{% /notice %}}
