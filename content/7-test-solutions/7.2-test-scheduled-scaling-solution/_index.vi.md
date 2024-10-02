---
title: "Kiểm thử giải pháp scheduled scaling"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>7.2. </strong>"
---

### Scheduled Scaling

Scheduled Scaling là mình sẽ cho ASG biết là khi nào, khoảng thời gian nào là nó nên khởi tạo thêm các instance và thời điểm nào là nó nên xoá bớt đi các instance. Loại scale này phù hợp cho các lượng công việc mà trong đó nó sẽ biến động theo một khoảng thời gian nhất định, có tính chất lặp lại từng ngày và trong một khoảng thời gian dài.

Vì ở phần trước thì chúng ta đã cài đặt phần kiểm thử rồi, nên giớ chúng ta sẽ không cần phải cài đặt lại nữa, tiếp tục dùng các thông số cài đặt đó.

#### Tiến hành cấu hình

Vào trong trang thông tin của ASG đã tạo, vào tab Automatic scaling, kéo xuống dưới cùng.

![7.2.1](/images/7-test-solution/7.2.1.png)

Ở dưới phần Scheduled actions, ấn **Create scheduled action**

![7.2.2](/images/7-test-solution/7.2.2.png)

Một biểu mẫu sẽ hiện lên, điền các thông tin như sau

- Name: `Rush hour`.
- Desired capacity: **1**.
- Min: **1** (các bạn nên để là 0).
- Max: **3**.
- Recurrence: **Once** (hoặc bất kì lựa chọn nào khác).
- Time zone: **Asia/Ho_Chi_Minh**.
- Specific start time: nên chỉnh thời gian gần nhất với lúc mà bạn đang cấu hình.
- Ấn **Create** để tạo.

![7.2.3](/images/7-test-solution/7.2.3.png)

{{% notice note %}}
Các thông số Desired capacity, Min hay Max nó đều sẽ ảnh hưởng tới các thông số tương ứng của ASG, nên trên thực tế thì chúng ta cũng sẽ cần phải kết hợp nhiều loại scaling và cân nhắc, xem xét kĩ lưỡng khi cấu hình các thông số này.
{{% /notice %}}

Đã tạo thành công.

![7.2.4](/images/7-test-solution/7.2.4.png)

#### Kiểm thử

Trước khi ASG khởi tạo instance theo lịch khoảng 5 phút, thì chúng ta nên chạy chương trình test.

![7.2.5](/images/7-test-solution/7.2.5.png)

Sau một vài phút, thời điểm ASG khởi tạo instance mới đã tới. Lúc này vào trong tab **Activity** để xem các hoạt động của ASG. Có thể thấy là sự kiện **Executing scheduled action Rush hour** được khởi động vào đúng thời điểm và sau đó thì ASG khởi tạo instance mới.

![7.2.6](/images/7-test-solution/7.2.6.png)

Trở lại với EC2 Console, các metrics sẽ được cập nhật vào mỗi 15 phút một lần, nên khi quay lại để quan sát các thông số này, tập chung vào biểu đồ CPU Utilization, thì chúng ta có thể thấy là từ khoảng 14:30 tới 14:40 thì có một đoạn bị gấp khúc và tăng cao, đó là khi mà chung ta mở chương trình test.

![7.2.7](/images/7-test-solution/7.2.7.png)

Đợt tiếp thêm vài phút để các metric này được cập nhật, khi được cập nhật thì tích chọn thêm instance vừa mới được khởi tạo.

![7.2.8](/images/7-test-solution/7.2.8.png)

Chúng ta có thể thấy là sau khúc 14:40 thì đường biểu đồ đã đi xuống.

Phóng to biểu đồ này lên

- Chọn **1h**
- Chọn **1 second**

![7.2.9](/images/7-test-solution/7.2.9.png)

Chúng ta sẽ thấy rõ hơn về sự thay đổi.

#### Kết luận

Trong thực tế thì các sàn giao dịch thường sẽ có các thời điểm mà lượng người dùng sẽ tăng cao. Và việc tăng cao này nó giống như giờ cao điểm ở giao thông, cứ vào một khoảng thời điểm nhất định nào đó thì lượng người tham gia giao thông / giao dịch sẽ tăng cao, việc này sẽ lặp lại vào mỗi ngày trong một thời gian dài. Khi đó thì mình sẽ cần lên lịch cho các instance mới để chịu tải.

Nhưng trong thực tế thì chúng ta cần sẽ phải kết hợp với các loại scaling khác để tăng độ tin cậy của hệ thống.
