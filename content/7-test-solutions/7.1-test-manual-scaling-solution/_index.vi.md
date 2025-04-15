---
title: "Kiểm thử giải pháp manual scaling"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>7.1. </strong>"
---

#### Manual Scaling

**ℹ️ Information**: Manual Scaling là phương pháp điều chỉnh thủ công thông số **Desired capacity** của Auto Scaling Group (ASG). Sau khi điều chỉnh và xác nhận cập nhật, ASG sẽ tự động khởi tạo hoặc xóa EC2 Instance dựa trên giá trị Desired capacity mới.

#### Cài đặt kiểm thử

Khi tạo xong Auto Scaling Group, dịch vụ này sẽ tự động khởi tạo một EC2 Instance theo cấu hình đã thiết lập. Để xác nhận điều này, chúng ta có thể vào EC2 Console:

- Chọn **Load Balancer**
- Chọn tab **Resource map - new**

Tại đây, chúng ta có thể thấy Target Group đang liên kết với 2 Targets (EC2 Instances): một instance gốc được tạo trước đó và một instance được tạo từ ASG.

![7.1.1](/images/7-test-solution/7.1.1.png)

**💡 Pro Tip**: Resource Map là công cụ trực quan giúp bạn dễ dàng theo dõi mối quan hệ giữa Load Balancer, Target Group và các EC2 Instance, đặc biệt hữu ích khi làm việc với Auto Scaling.

Tiếp theo, chúng ta sẽ kiểm thử với ứng dụng đã tải trước đó:

- Mở ứng dụng, chọn tab **Test Type**
- Test Type:
  - Chọn **CLICKS**
  - Run until: **100000**
- User Simulation
  - Number Of Users: **1000**
  - Click Delay: **1** seconds

![7.1.2](/images/7-test-solution/7.1.2.png)

Trong tab URLs, cấu hình các thông tin:

- Name: `Manual Scaling Test` (bạn có thể đặt tên tùy ý, vì chúng ta sẽ sử dụng lại cho các loại scaling khác sau này)
- URL: Dán DNS của Load Balancer vào đây

![7.1.3](/images/7-test-solution/7.1.3.png)

Trên thanh công cụ, nhấn **Start Test** để bắt đầu.

![7.1.4](/images/7-test-solution/7.1.4.png)

#### Tiến hành kiểm thử

Quay lại AWS Management Console, vào EC2 Console:

- Tích chọn 2 EC2 Instance trong target group
- Chọn tab **Monitoring** và bắt đầu quan sát

**ℹ️ Information**: Trong phần Monitoring, chúng ta sẽ tập trung vào 5 biểu đồ quan trọng sau:

1. **CPU Utilization (%)**: Hiển thị lượng tài nguyên CPU mà mỗi instance đã sử dụng (khoảng dưới 8%)
2. **Network in (bytes)**: Hiển thị dung lượng mạng đi vào mỗi instance (khoảng dưới 2.9 triệu Megabytes)
3. **Network out (bytes)**: Hiển thị dung lượng mạng đi ra từ mỗi instance (khoảng dưới 17.3 triệu Megabytes)
4. **Network packets in (count)**: Hiển thị số lượng gói tin đi vào mỗi instance (khoảng dưới 6.85 nghìn gói tin)
5. **Network packets out (count)**: Hiển thị số lượng gói tin đi ra từ mỗi instance (khoảng dưới 7.36 nghìn gói tin)

![7.1.5](/images/7-test-solution/7.1.5.png)

{{% notice note %}}
Từ giờ trở đi chúng ta sẽ đọc các biểu đồ này như vậy. Bao gồm các thông số quan trọng ở cột dọc, cột ngang và các đường vẽ. Từ đây sẽ giúp chúng ta hiểu hơn về cách Load Balancer cân bằng lưu lượng mạng tới cho các instance ở trong Target Group.
{{% /notice %}}

{{% notice note %}}
Nếu bạn chỉ tích chọn 1 instance, thì trên biểu đồ chỉ có một đường vẽ đại diện cho instance đó. Khi tích chọn càng nhiều instance trên danh sách, sẽ càng có nhiều đường biểu diễn hơn.
{{% /notice %}}

#### Điều chỉnh thủ công thông số Desired capacity của ASG

Trở lại trang thông tin chi tiết của ASG đã tạo trước đó. Trong phần Group details, chúng ta thấy: **Desired capacity = 1**.

**ℹ️ Information**: Giả sử một tình huống đã qua giờ cao điểm và chúng ta muốn tắt bớt một instance để tiết kiệm chi phí. Để thực hiện, chúng ta sẽ điều chỉnh thủ công thông số **Desired capacity = 0**. Nhấn **Edit**.

![7.1.6](/images/7-test-solution/7.1.6.png)

**⚠️ Warning**: Khi giảm Desired capacity xuống 0, tất cả các instance do ASG quản lý sẽ bị chấm dứt. Đảm bảo rằng đây là hành động có chủ đích và sẽ không ảnh hưởng đến tính khả dụng của ứng dụng.

Trong bảng thông tin Group size, điều chỉnh Desired capacity và Min desired capacity về **0** và nhấn **Update**.

![7.1.7](/images/7-test-solution/7.1.7.png)

Sau đó vào tab Activity để xem hoạt động của ASG.

![7.1.8](/images/7-test-solution/7.1.8.png)

{{% notice note %}}
Trong quá trình instance đang được tắt đi, bạn có thể tạm dừng chương trình test.
{{% /notice %}}

**ℹ️ Information**: Như vậy, chúng ta có thể thấy ASG sẽ tự động hủy instance theo thông số đã được cấu hình.

Sau vài phút, vào lại trang thông tin của Load Balancer, chọn tab **Resource map - new**, chúng ta sẽ thấy giờ chỉ còn một target.

![7.1.9](/images/7-test-solution/7.1.9.png)

{{% notice note %}}
Tới bước này, hãy BẬT LẠI chương trình test.
{{% /notice %}}

**ℹ️ Information**: Chúng ta cũng sẽ nhận được email thông báo từ Amazon SNS về việc ASG đã chấm dứt instance.

![7.1.10](/images/7-test-solution/7.1.10.png)

**💡 Pro Tip**: Thông báo SNS giúp bạn theo dõi các hoạt động của ASG trong thời gian thực, đặc biệt hữu ích khi triển khai các chiến lược scaling trong môi trường sản xuất.

Khi chương trình đang có lưu lượng truy cập lớn, các thao tác sẽ bị chậm đi. Bạn có thể mở ứng dụng thông qua DNS của Load Balancer để kiểm thử.

![7.1.11](/images/7-test-solution/7.1.11.png)

Quay lại EC2 Console, chọn target còn lại và quan sát biểu đồ.

![7.1.12](/images/7-test-solution/7.1.12.png)

**ℹ️ Information**: Có thể thấy, hiện tại instance đang phải chịu tải lưu lượng mạng vào và ra gần như gấp đôi, và lượng tài nguyên CPU đã sử dụng gần gấp 4 lần so với trước đó.

#### Kết luận

**💡 Pro Tip**: Trên thực tế, các hệ thống sẽ có các quy trình xử lý phức tạp hơn, thời gian xử lý lâu hơn, do đó sẽ tiêu tốn nhiều tài nguyên CPU hơn. Trong bài lab này, chúng ta chỉ kiểm tra giao thức GET đơn giản, trong khi các ứng dụng thực tế sẽ có các request phức tạp hơn nhiều.

**🔒 Security Note**: Khi thực hiện manual scaling trong môi trường sản xuất, cần đảm bảo rằng việc giảm số lượng instance không ảnh hưởng đến khả năng xử lý của hệ thống và không tạo ra các điểm yếu về bảo mật do quá tải.
