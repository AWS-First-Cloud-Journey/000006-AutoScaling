---
title: "Kiểm thử giải pháp manual scaling"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>7.1. </strong>"
---

### Manual Scaling

Manual Scaling là mình sẽ thực hiện bằng cách là tự điều chỉnh thủ công thông số **Desired capacity** của ASG, sau khi điều chỉnh xong và xác nhận update thì đợi trong một khoảng thời gian, ASG sẽ update xong số lượng và tiến hành khởi tạo hoặc xoá bớt đi EC2 Instance tuỳ thuộc vào thông số **Desired capacity** đó.

#### Cài đặt kiểm thử

Khi tạo xong Auto Scaling Group, thì chính dịch vụ này sẽ tự động khởi tạo một EC2 Instance do chúng ta cấu hình trước đó, để có thể xem được điều này thì chúng ta có thể vào trong EC2 Console

- Chọn **Load Balancer**
- Chọn tab **Resource map - new**

Ở đây chúng ta có thể thấy được là Target Group trước đó đang có liên kết tới 2 Targets lần lượt là 2 EC2 Instances (1 là instance gốc được tạo trước đó; cái còn lại là instance được tạo từ ASG).

![7.1.1](/images/7-test-solution/7.1.1.png)

Giờ thì kiểm thử với ứng dụng mà chúng ta đã tải trước đó.

- Mở ứng dụng lên, ấn vào tab **Test Type**
- Test Type:
  - Chọn **CLICKS**
  - Run until: **100000**
- User Simulation
  - Number Of Users: **1000**
  - Click Delay: **1** seconds

![7.1.2](/images/7-test-solution/7.1.2.png)

Trong tab URLs, mình sẽ cấu hình các thông tin

- Name: `Manual Scaling Test`, ở đây thì bạn đặt là gì cũng được, bởi vì chúng ta sẽ dùng để test trong các loại scaling khác sau đó.
- URL: copy DNS của Load Balancer và dán vào.

![7.1.3](/images/7-test-solution/7.1.3.png)

Trên thanh công cụ, mình sẽ bắt đầu ấn **Start Test**.

![7.1.4](/images/7-test-solution/7.1.4.png)

#### Tiến hành kiểm thử

Giờ quay lại với AWS Management Console, vào trong EC2 Console

- Tích chọn 2 EC2 Instance ở trong target group
- Ấn vào tab **Monitoring** và bắt đầu quan sát

Trong mục này, chúng ta có 7 biểu đồ, nhưng hiện tại thì chúng ta chỉ quan tâm tới 5 biểu đồ sau:

- CPU Utilization (%): biểu đồ cho thấy lượng tài nguyên CPU mà 2 instances này đã dùng trong khoảng dưới 8% với mỗi instance.
- Network in (bytes): biểu đồ cho thấy dung lượng mạng đi vào 2 instances này trong khoảng dưới 2.9 triệu Megabytes với mỗi instance.
- Network out (bytes): biểu đồ cho thấy dung lượng mạng đi ra từ 2 instances này trong khoảng dưới 17.3 triệu Megabytes với mỗi instance.
- Network packets in (count): biểu đồ cho thấy số lượng các gói tin đi vào 2 instances này trong khoảng dưới 6.85 nghìn gói tin với mỗi instance.
- Network packets out (count): biểu đồ cho thấy số lượng các gói tin đi ra từ 2 instances này trong khoảng dưới 7.36 nghìn gói tin với mỗi instance.

![7.1.5](/images/7-test-solution/7.1.5.png)

{{% notice note %}}
Từ giờ trở đi chúng ta sẽ đọc các biểu đồ này như vậy. Bao gồm các thông số quan trọng ở cột dọc, cột ngang và các đường vẽ. Từ đây sẽ giúp chúng ta hiểu hơn về cách Load Balancer cân bằng lưu lượng mạng tới cho các instance ở trong Target Group.
{{% /notice %}}

{{% notice note %}}
Và nếu như mà bạn chỉ tích chọn 1 instance, thì trên biểu đồ chỉ có một đường vẽ đại diện cho instance đó. Như vậy, khi tích chọn càng nhiều trên danh sách thì sẽ càng có nhiều đường biểu diễn hơn.
{{% /notice %}}

#### Điều chính thủ công thông số Desired capacity của ASG

Giờ thì chúng ta trở lại với trang thông tin chi tiết của ASG mà chúng ta đã tạo ở trước đó. Trong phần Group details, chúng ta có thể thấy được là: **Desired capacity = 1**.

Giờ chúng ta sẽ giả sử một tình huống, là đã qua giờ cao điểm nên là mình muốn tắt bớt đi một instance để tiết kiệm chi phí. Để làm được việc này thì chúng ta sẽ điều chỉnh thủ công thông số **Desired capacity = 0**. Ấn **Edit**.

![7.1.6](/images/7-test-solution/7.1.6.png)

Sẽ hiện lên bảng thông tin Group size, điều chỉnh Desired capacity và Min desired capacity về **0** và ấn **Update**.

![7.1.7](/images/7-test-solution/7.1.7.png)

Sau đó vào trong tab Activity để xem ASG đang có hoạt động gì.

![7.1.8](/images/7-test-solution/7.1.8.png)

{{% notice note %}}
Trong quá trình instance đang được tắt đi, thì bạn có thể dừng chương trình test lại.
{{% /notice %}}

=> Như vậy chúng ta có thể thấy là ASG sẽ tự động huỷ đi một instance theo như thông số mà nó đã được cấu hình.

Một vài phút sau, vào lại trong trang thông tin của Load Balancer, vào tab **Resource map - new** thì chúng ta có thể thấy được là giờ chỉ còn có một target thôi.

![7.1.9](/images/7-test-solution/7.1.9.png)

{{% notice note %}}
Tới bước này thì bạn NHỚ BẬT LẠI chương trình test.
{{% /notice %}}

Chúng ta cũng sẽ nhận được một email từ SNS

![7.1.10](/images/7-test-solution/7.1.10.png)

Khi chương trình của chúng ta đang có lưu lượng truy cập lớn, thì thao tác sẽ bị chậm đi một ít. Các bạn có thể mở ứng dụng thông qua DNS của Load Balancer để kiểm thử.

![7.1.11](/images/7-test-solution/7.1.11.png)

Giờ thì vào lại EC2 Console, chọn target còn lại, và quan sát biểu đồ.

![7.1.12](/images/7-test-solution/7.1.12.png)

Có thể thấy, hiện tại thì instance đã chịu tải lưu lượng mạng vào và ra có thể nói là gấp đôi và lượng tài nguyên CPU đã dùng gần gấp 4 lần.

#### Kết luận

Trên thực tế thì các hệ thống sẽ có các bước thực hiện phức tạp hơn, lâu hơn nên từ đó sẽ dùng nhiều tài nguyên CPU hơn. Trong bài này thì chúng ta chỉ kiểm tra giao thực GET, còn thực tế thì các request này sẽ phức tạp hơn nhiều.
