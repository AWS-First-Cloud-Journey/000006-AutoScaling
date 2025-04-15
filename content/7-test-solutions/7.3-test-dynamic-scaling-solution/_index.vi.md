---
title: "Kiểm thử giải pháp dynamic scaling"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>7.3. </strong>"
---

#### Dynamic Scaling

**ℹ️ Information**: Dynamic Scaling là phương pháp tự động điều chỉnh số lượng EC2 Instance dựa trên các metrics được cung cấp bởi Amazon CloudWatch. Auto Scaling Group (ASG) sẽ tự động khởi tạo hoặc kết thúc các instance dựa trên các ngưỡng metric đã được cấu hình. Chúng ta có thể thiết lập ASG để tạo instance mới khi tài nguyên CPU vượt quá 90%, khi lưu lượng mạng tăng cao, hoặc khi số lượng request trên mỗi target vượt quá ngưỡng xác định.

Tùy thuộc vào đặc thù hệ thống và yêu cầu ứng dụng, chúng ta sẽ lựa chọn metric phù hợp để cấu hình. Trong bài lab này, chúng ta sẽ cấu hình Dynamic Scaling dựa trên "số lượng request được gửi đến mỗi target".

#### Tiến hành cấu hình

Trước khi bắt đầu kiểm thử, chúng ta sẽ thực hiện scale in thủ công để giảm số lượng instance. Vào tab **Activity** của ASG để theo dõi quá trình này.

![7.3.1](/images/7-test-solution/7.3.1.png)

![7.3.2](/images/7-test-solution/7.3.2.png)

Sau khi đã giảm số lượng instance, chúng ta sẽ cấu hình Dynamic Scaling. Vào tab **Automatic scaling**:

- Nhấn **Create dynamic scaling policy** để tạo chính sách scaling tự động mới

![7.3.3](/images/7-test-solution/7.3.3.png)

Điền các thông số vào biểu mẫu như sau:

- Policy type: **Target tracking scaling**
- Scaling policy name: `Request Over 500 per target`
- Metric type: **Application Load Balancer request count per target**
- Target group: **FCJ-Management-TG**
- Target value: **500** (requests)
- Instance warmup: **60 seconds** (nên cấu hình cao hơn trong môi trường sản xuất)
- Nhấn **Create** để hoàn tất

![7.3.4](/images/7-test-solution/7.3.4.png)

{{% notice info %}}
Thông số **Instance warmup** xác định khoảng thời gian mà một instance mới cần để đạt trạng thái hoạt động ổn định trước khi bắt đầu nhận lưu lượng từ Load Balancer. Khi một instance chuyển sang trạng thái **InService**, ASG sẽ chờ hết thời gian warmup trước khi đưa instance vào xử lý requests. Việc cấu hình thông số này hợp lý giúp đảm bảo instance có đủ thời gian để khởi động ứng dụng, cài đặt các phụ thuộc, và thiết lập kết nối đến các dịch vụ khác trước khi xử lý lưu lượng người dùng.
{{% /notice %}}

Kết quả sau khi tạo chính sách:

![7.3.5](/images/7-test-solution/7.3.5.png)

#### Kiểm thử

Bắt đầu chạy chương trình kiểm thử để tạo tải:

![7.3.6](/images/7-test-solution/7.3.6.png)

Vào EC2 Console để theo dõi lưu lượng request đến các EC2 Instance:

![7.3.7](/images/7-test-solution/7.3.7.png)

{{% notice note %}}
Cần chờ một khoảng thời gian để CloudWatch metrics được cập nhật. Sau đó, bạn sẽ thấy các biểu đồ có xu hướng tăng và dần ổn định.
{{% /notice %}}

Quay lại tab **Activity** của ASG, chúng ta sẽ thấy có 3 instances được tạo. Do lượng request rất lớn, ASG đã tính toán và tạo ra số lượng instance tối đa theo cấu hình Max capacity:

![7.3.8](/images/7-test-solution/7.3.8.png)

Trở lại EC2 Console, tích chọn tất cả các instances được tạo ra và quan sát các biểu đồ metrics:

![7.3.9](/images/7-test-solution/7.3.9.png)

Bạn sẽ thấy đường màu xanh (instance ban đầu) đang dần giảm xuống, trong khi các đường khác (instance mới) đang xuất hiện và nhận lưu lượng.

{{% notice note %}}
CloudWatch metrics thường được cập nhật khoảng 15 phút một lần, vì vậy bạn cần chờ một khoảng thời gian để thấy được kết quả đầy đủ và chính xác.
{{% /notice %}}

Giờ chúng ta sẽ tắt chương trình kiểm thử:

![7.3.10](/images/7-test-solution/7.3.10.png)

Vào tab **Activity** của ASG và theo dõi quá trình ASG tự động kết thúc các instance không còn cần thiết. Quá trình này có thể mất một khoảng thời gian.

![7.3.11](/images/7-test-solution/7.3.11.png)

#### Kết luận

**ℹ️ Information**: Khi ASG phát hiện hệ thống có dấu hiệu quá tải dựa trên các metrics đã cấu hình, nó sẽ tự động khởi tạo thêm một hoặc nhiều instance để đưa hệ thống về trạng thái ổn định. Tuy nhiên, Dynamic Scaling có độ trễ nhất định do phụ thuộc vào chu kỳ cập nhật của CloudWatch metrics và thời gian khởi tạo instance mới.

**💡 Pro Tip**: Để cải thiện khả năng phản ứng của hệ thống trước các đợt tăng tải đột ngột, nên kết hợp Dynamic Scaling với Predictive Scaling. Predictive Scaling giúp ASG dự đoán trước các mô hình lưu lượng và chuẩn bị capacity từ trước, giúp hệ thống phản ứng nhanh hơn với các thay đổi lưu lượng.
