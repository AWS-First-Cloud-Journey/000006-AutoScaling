---
title: "Kiểm tra kết quả"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: "<strong>5. </strong>"
---

### Kiểm tra kết quả

Sau khi triển khai xong Load Balancer, thì chúng ta sẽ lấy DNS name của LB này và dán vào trong trình duyệt để thử kết quả của triển khai.

![5.1.png](/images/5-test/5.1.png)

Và đây là kết quả

![5.2.png](/images/5-test/5.2.png)

Giờ thì chúng ta sẽ thao tác một số thứ để kiểm tra xem hệ thống hoạt động ổn định hay không. Thử thay đổi thông tin của 1 record.

![5.3.png](/images/5-test/5.3.png)

Khi nhập xong thì chúng ta ấn Submit và nhận được thông báo.

![5.4.png](/images/5-test/5.4.png)

Trở lại trang chủ và nhận được kết quả là

![5.5.png](/images/5-test/5.5.png)

Ở các bước kiểm thử ở sau, thì chúng ta sẽ đọc các metrics là chính, nhưng bạn cũng có thể vừa đọc và vừa kiểm tra xem là ứng dụng có bị chậm trong quá trình kiểm thử hay không.
