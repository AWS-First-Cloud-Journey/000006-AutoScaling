---
title: "Triển khai ứng dụng FCJ Management với Auto Scaling Group"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

# Triển khai ứng dụng FCJ Management với Auto Scaling Group

#### Tổng quan

Trong hướng dẫn này, chúng ta sẽ thực hiện triển khai ứng dụng bằng cách sử dụng Amazon EC2 Auto Scaling Group để đảm bảo khả năng mở rộng linh hoạt theo nhu cầu của người truy cập. Ngoài ra, chúng ta cũng sẽ triển khai Elastic Load Balancing để cân bằng tải và phân phối yêu cầu từ người dùng đến Application Tier của ứng dụng.

**ℹ️ Information**: Hãy đảm bảo bạn đã xem qua tài liệu [Triển khai Ứng dụng FCJ Management trên Máy ảo Windows/Amazon Linux](https://000004.awsstudygroup.com/) để nắm vững cách triển khai ứng dụng trên máy ảo. Chúng ta sẽ cần sử dụng máy ảo **FCJ Management** đã triển khai để thực hiện việc triển khai đồng loạt và mở rộng trong Auto Scaling Group.


#### Nội dung

1. [Giới thiệu](1-introduction/)
2. [Các bước chuẩn bị](2-preparation/)
3. [Khởi tạo Launch Template](3-create-launch-template/)
4. [Thiết lập Elastic Load Balancer](4-setup-load-balancer/)
5. [Kiểm thử](5-test/)
6. [Khởi tạo Auto Scaling Group](6-create-auto-scaling-group/)
7. [Kiểm thử các giải pháp](7-test-solutions/)
8. [Dọn dẹp tài nguyên](8-cleanup/)

#### Lợi ích của Auto Scaling Group

Auto Scaling Group (ASG) mang lại nhiều lợi ích quan trọng khi triển khai ứng dụng trên AWS:

1. **Tính sẵn sàng cao**: ASG tự động thay thế các instance bị lỗi, đảm bảo ứng dụng luôn sẵn sàng phục vụ người dùng.

2. **Khả năng mở rộng linh hoạt**: Tự động tăng hoặc giảm số lượng instance dựa trên nhu cầu thực tế, giúp tối ưu chi phí vận hành.

3. **Phân phối tải hiệu quả**: Kết hợp với Elastic Load Balancer, ASG giúp phân phối đều tải giữa các instance, tránh quá tải cho một máy chủ cụ thể.

4. **Tiết kiệm chi phí**: Chỉ sử dụng đúng số lượng tài nguyên cần thiết, tránh lãng phí khi lưu lượng truy cập thấp.

5. **Tự động hóa cao**: Giảm thiểu sự can thiệp thủ công trong việc quản lý cơ sở hạ tầng.

Trong workshop này, bạn sẽ được thực hành triển khai và cấu hình các loại scaling khác nhau, từ đó hiểu rõ cách áp dụng ASG vào các tình huống thực tế.

