---
title: "Kiểm thử giải pháp dynamic scaling"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>7.3. </strong>"
---

### Dynamic Scaling

Dynamic scaling là dạng mà nó sẽ dựa vào các metric được cung cấp bởi CloudWatch, khi này thì tuỳ thuộc vào việc mà chúng ta cấu hình thì nó sẽ khởi tạo và huỷ instance đi. Chúng ta có thể cấu hình sao cho ASG sẽ mở một instance mới khi tài nguyên CPU của instance hoặc các instance ở trên mức 90% hoặc là lưu lượng mạng và và ra lớn hoặc là số các gói tin gửi tới từng instance là lớn.

Tuỳ vào hệ thống và tính chất thì chúng ta sẽ cấu hình khác đi. Trong bài này, chúng ta sẽ cấu hình theo dạng "số lượng các gói tin được gửi tới từng instance".

#### Tiến hành cấu hình

Trước khi kiểm thử, thì mình sẽ tiến hành scale in thủ công, giảm bớt đi một instance, khi đó thì vào trong tab Activity và kiểm tra lại.

![7.3.1](/images/7-test-solution/7.3.1.png)

![7.3.2](/images/7-test-solution/7.3.2.png)

Sau khi đã xoá xong thì giờ chúng ta sẽ cấu hình Dynamic. Vào trong tab **Automatic scaling**

- Ấn **Create dynamic scaling policy** để tạo chính sách scaling tự động mới.

![7.3.3](/images/7-test-solution/7.3.3.png)

Trong biểu mẫu này thì chúng ta sẽ điền các thông số như sau:

- Policy type: **Target tracking scaling**.
- Scaling policy name: `Request Over 500 per target`.
- Metric type: **Application Load Balancer request count per target**.
- Target group: **FCJ-Management-TG**.
- Target value: **500** (requests).
- Instance warmup: **60 seconds** (nên để số lớn hơn).
- Ấn **Create** để tạo.

![7.3.4](/images/7-test-solution/7.3.4.png)

{{% notice info %}}
Thông số **Instance warmup** sẽ ảnh hưởng tới thời gian mà instance sẽ bắt đầu nhận các lưu lượng từ bên ngoài vào. Cụ thể là khi mà một instance được tạo và và trong trạng thái **InSeriver** (sẵn sàng để hoạt động) thì chúng ta có thể điều chỉnh khoảng thời gian để một instance bắt đầu nhận và xử lý các requests từ bên ngoài, khoảng thời gian đó gọi là **instance warmup**. Việc điều chỉnh thông số này là để kéo thêm thời gian cho instance đi vào hoạt động ổn định hoàn toàn, vì ứng dụng cần phải cập nhật và cài đặt các phụ thuộc khác cũng như là kết nối tới các dịch vụ khác để có thể hoạt động bình thường.
{{% /notice %}}

Kết quả

![7.3.5](/images/7-test-solution/7.3.5.png)

#### Kiểm thử

Bắt đầu chạy chương trình kiểm thử

![7.3.6](/images/7-test-solution/7.3.6.png)

Vào trong EC2 Console để xem lưu lượng request tới EC2 là bao nhiêu

![7.3.7](/images/7-test-solution/7.3.7.png)

{{% notice note %}}
Chờ một xíu để metrics được cập nhật và chúng ta có thể thấy là các biểu đồ có xu hướng đi lên và đi ngang.
{{% /notice %}}

Vào lại trong tab **Activity** của ASG, chúng ta sẽ thấy có 3 instances được tạo. Bởi vì lượng request là rất lớn, nên ASG tính toán được là nó cần sẽ phải tạo tối đa số instances mong muốn.

![7.3.8](/images/7-test-solution/7.3.8.png)

Trở lại với EC2 Console, tích chọn tất cả các instances được tạo ra, và quan sát các biểu đồ

![7.3.9](/images/7-test-solution/7.3.9.png)

Chúng ta sẽ thấy được là đường màu xanh đang dần đi xuống, và các đường khác đang dần được hiện ra.

{{% notice note %}}
Như mình đã nói ở phần trước thì các thông số sẽ được cập nhật khoảng 15 phút một lần, vì thế mà bạn sẽ cần phải chờ một khoảng thời gian để thấy được kết quả.
{{% /notice %}}

Giờ thì chúng ta sẽ tắt chương trình kiểm thử.

![7.3.10](/images/7-test-solution/7.3.10.png)

Vào trong tab Activity của ASG và chờ ASG huỷ các instance không còn cần thiết nữa, quá trình này có thể sẽ khá lâu.

![7.3.11](/images/7-test-solution/7.3.11.png)

#### Kết luận

Khi ASG nhận thấy được là hệ thống đang có dấu hiệu quá tải từ một hoặc nhiều thông số nào đó, thì nó sẽ tiến hành khởi tạo thêm một hoặc nhiều instance để cho hệ thống trở về trạng thái ổn định. Nhưng dynamic scaling sẽ không được nhanh cho lắm bởi vì như mình đã nói ở trên, khi các chính sách scaling được tạo ra thì nó sẽ ảnh hưởng, tới các thông số gốc, từ đó ASG sẽ "nhìn" vào đó mà lựa chọn việc mở rộng hoặc thu gọn.

Nên số lượng các instance sẽ được tính toán và cập nhật lại cũng không được nhanh cho lắm. Với vấn đề này thì chúng ta sẽ có một giải pháp khác đi kèm là Predictive Scaling, để khi đó ASG sẽ phản ứng nhanh hơn.
