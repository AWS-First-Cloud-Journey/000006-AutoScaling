---
title: "Kiểm thử giải pháp scheduled scaling"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>7.2. </strong>"
---

#### Scheduled Scaling

**ℹ️ Information**: Scheduled Scaling cho phép bạn cấu hình Auto Scaling Group (ASG) để tự động điều chỉnh số lượng instance theo lịch trình đã định sẵn. Giải pháp này phù hợp với các workload có tính chu kỳ, biến động theo thời gian cụ thể và lặp lại theo quy luật trong thời gian dài.

Vì đã cài đặt phần kiểm thử ở phần trước, chúng ta sẽ tiếp tục sử dụng các thông số cài đặt đó mà không cần cấu hình lại.

#### Tiến hành cấu hình

Truy cập vào trang thông tin chi tiết của ASG đã tạo, chọn tab **Automatic scaling**, sau đó kéo xuống phần cuối trang:

![7.2.1](/images/7-test-solution/7.2.1.png)

Trong phần Scheduled actions, nhấn **Create scheduled action**:

![7.2.2](/images/7-test-solution/7.2.2.png)

Điền các thông tin vào biểu mẫu như sau:

- Name: `Rush hour`
- Desired capacity: **1**
- Min: **1** (**💡 Pro Tip**: Nên cấu hình là 0 trong môi trường thực tế để tối ưu chi phí)
- Max: **3**
- Recurrence: **Once** (hoặc lựa chọn khác phù hợp với nhu cầu)
- Time zone: **Asia/Ho_Chi_Minh**
- Specific start time: Chọn thời gian gần nhất với thời điểm hiện tại
- Nhấn **Create** để hoàn tất

![7.2.3](/images/7-test-solution/7.2.3.png)

{{% notice note %}}
Các thông số Desired capacity, Min và Max sẽ ảnh hưởng trực tiếp đến cấu hình tương ứng của ASG. Trong môi trường sản xuất, cần kết hợp nhiều loại scaling và cân nhắc kỹ lưỡng khi thiết lập các thông số này.
{{% /notice %}}

Sau khi tạo thành công, bạn sẽ thấy scheduled action mới trong danh sách:

![7.2.4](/images/7-test-solution/7.2.4.png)

#### Kiểm thử

**⚠️ Warning**: Nên bắt đầu chạy chương trình kiểm thử khoảng 5 phút trước khi ASG dự kiến khởi tạo instance theo lịch trình để có thể quan sát đầy đủ hiệu quả của scheduled scaling.

![7.2.5](/images/7-test-solution/7.2.5.png)

Sau vài phút, khi thời điểm đã đến, vào tab **Activity** để theo dõi các hoạt động của ASG. Bạn sẽ thấy sự kiện **Executing scheduled action Rush hour** được kích hoạt đúng thời điểm đã cấu hình, sau đó ASG sẽ khởi tạo instance mới:

![7.2.6](/images/7-test-solution/7.2.6.png)

**ℹ️ Information**: Quay lại EC2 Console để quan sát các metrics. Lưu ý rằng các metrics được cập nhật 15 phút một lần. Khi xem biểu đồ CPU Utilization, bạn có thể thấy đoạn gấp khúc và tăng cao từ khoảng 14:30 đến 14:40, đây là thời điểm chúng ta chạy chương trình kiểm thử:

![7.2.7](/images/7-test-solution/7.2.7.png)

Đợi thêm vài phút để các metrics được cập nhật đầy đủ, sau đó tích chọn thêm instance vừa được khởi tạo:

![7.2.8](/images/7-test-solution/7.2.8.png)

**💡 Pro Tip**: Để quan sát chi tiết hơn, bạn có thể phóng to biểu đồ bằng cách:
- Chọn **1h** cho khung thời gian
- Chọn **1 second** cho độ phân giải

![7.2.9](/images/7-test-solution/7.2.9.png)

Với cài đặt này, bạn sẽ thấy rõ hơn sự thay đổi trong hiệu suất hệ thống trước và sau khi instance mới được thêm vào.

#### Kết luận

**ℹ️ Information**: Trong môi trường thực tế, nhiều hệ thống như sàn giao dịch thường có các thời điểm lưu lượng người dùng tăng cao theo quy luật. Hiện tượng này tương tự như "giờ cao điểm" trong giao thông - vào những khoảng thời gian nhất định, lượng người tham gia giao dịch tăng đột biến và lặp lại hàng ngày trong thời gian dài. Scheduled Scaling giúp chuẩn bị trước các instance để đáp ứng nhu cầu tăng cao này.

**🔒 Security Note**: Mặc dù Scheduled Scaling rất hiệu quả cho các workload có tính chu kỳ, trong thực tế nên kết hợp với các loại scaling khác như Dynamic Scaling để tăng độ tin cậy và khả năng đáp ứng của hệ thống trước các biến động không lường trước được.
