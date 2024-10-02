---
title: "Giới thiệu"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>1. </strong>"
---

#### Giới thiệu 
Trong bài thực hành này, chúng ta sẽ tiến hành triển khai ứng dụng sử dụng Auto Scaling Group để đảm bảo khả năng mở rộng linh hoạt theo nhu cầu của người dùng. Chúng ta cũng sẽ triển khai Load Balancer để cân bằng tải và phân phối yêu cầu truy cập từ người dùng đến Application Tier.

Hãy đảm bảo bạn đã tham khảo tài liệu [Triển khai Ứng dụng FCJ Management trên Máy ảo Windows/AmazonLinux](https://000004.awsstudygroup.com/) và hiểu cách triển khai ứng dụng trên máy ảo. Chúng ta sẽ sử dụng máy ảo **FCJ Management** đã triển khai để thực hiện việc triển khai và mở rộng trong Auto Scaling Group.

#### Auto Scaling Group
1. Tại sao cần sử dụng Auto scaling group?
   
   Khi ứng dụng của chúng ta đưa vào hoạt động, lượng người truy cập sẽ thay đổi theo thời gian, do đó chúng ta cần thường xuyên thay đổi (scaling) lượng instance nhằm nâng cao tính sẵn sàng và tiết kiệm chi phí. Để tự động hóa và linh hoạt trong công việc scaling, chúng ta sẽ có giải pháp là Auto scaling group.
2. Sơ lược về Auto scaling group
   
    **Auto Scaling Group (ASG)** giúp tự động điều chỉnh số lượng EC2 instances theo nhu cầu của ứng dụng. ASG có thể tự động mở rộng (scale up) khi lưu lượng tăng, hoặc thu nhỏ (scale down) khi lưu lượng giảm, giúp tối ưu hóa tài nguyên và giảm chi phí. Nó cũng giúp đảm bảo tính sẵn sàng cao bằng cách phân phối instances qua nhiều Availability Zones để duy trì hoạt động liên tục ngay cả khi một phần của hệ thống gặp sự cố.
3. Các loại Scaling trong ASG
   
   Trong nội dung này, chúng ta sẽ tìm hiểu về các loại Scaling sau đây:
   - **Manual Scaling**: Người dùng tự tay điều chỉnh số lượng EC2 instances trong Auto Scaling Group dựa trên yêu cầu. Đây là phương pháp thủ công, không tự động dựa trên chỉ số cụ thể.
   - **Dynamic Scaling**: Tự động điều chỉnh số lượng instances dựa trên các chỉ số thời gian thực như CPU utilization, network traffic, hoặc custom metrics từ CloudWatch. Dynamic scaling có 3 chính sách chính là **Target Tracking Scaling**, **Step Scaling**, **Simple Scaling**.
   - **Scheduled Scaling**: Cho phép chúng ta cấu hình các thời gian cụ thể để tự động mở rộng hoặc thu nhỏ instances, ví dụ như tăng số lượng instances vào giờ cao điểm hoặc giảm xuống ngoài giờ làm việc. Phù hợp cho các trường hợp mà chúng ta đã biết trước mô hình lưu lượng truy cập.
   - **Predictive Scaling**: Nó dự đoán hoạt động bằng cách phân tích load data trong lịch sử để tìm các mẫu hàng ngày hoặc hàng tuần trong luồng lưu lượng truy cập. Nó sử dụng thông tin này để dự báo nhu cầu công suất trong tương lai để Amazon EC2 Auto Scaling có thể chủ động tăng công suất của Auto Scaling group để phù hợp với dự kiến.

#### Launch Template

**Launch Template** là một cấu hình chứa các thông số cần thiết để khởi chạy EC2 instances. Nó lưu trữ các chi tiết như loại instance, AMI (Amazon Machine Image), key pair, network settings, security groups, và các thông tin khác về cấu hình của EC2. Nhằm đơn giản hóa việc tạo instance, hỗ trợ trong việc tự động tạo mới các instance trong ASG.

#### Elastic Load Balancer

**Elastic Load Balancer** là một công cụ giúp phân phối đều tải công việc (traffic) đến nhiều máy chủ hoặc instances để đảm bảo hệ thống hoạt động ổn định và tránh quá tải cho bất kỳ một máy chủ nào. Nó giúp tối ưu hiệu suất, tăng tính sẵn sàng và đảm bảo rằng nếu một máy chủ gặp sự cố, lưu lượng sẽ được chuyển hướng tới các máy chủ khác mà không ảnh hưởng đến người dùng.

#### Target Group

**Target Group** là một thành phần của Elastic Load Balancer (ELB), dùng để xác định và quản lý các EC2 instances mà Load Balancer sẽ phân phối lưu lượng truy cập đến.

