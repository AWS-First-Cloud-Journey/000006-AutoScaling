---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

# Giới thiệu

Trong bài thực hành này, chúng ta sẽ tiến hành triển khai ứng dụng sử dụng Auto Scaling Group để đảm bảo khả năng mở rộng linh hoạt theo nhu cầu của người dùng. Chúng ta cũng sẽ triển khai Load Balancer để cân bằng tải và phân phối yêu cầu truy cập từ người dùng đến Application Tier.

Hãy đảm bảo bạn đã tham khảo tài liệu [Triển khai Ứng dụng FCJ Management trên Máy ảo Windows/AmazonLinux](https://000004.awsstudygroup.com/) và hiểu cách triển khai ứng dụng trên máy ảo. Chúng ta sẽ sử dụng máy ảo **FCJ Management** đã triển khai để thực hiện việc triển khai và mở rộng trong Auto Scaling Group.

## Auto Scaling Group

**Auto Scaling Group** (Nhóm co giãn tự động) là một nhóm các EC2 Instance. Nhóm này có khả năng co giãn số lượng các EC2 Instance thành viên dựa trên các chính sách co giãn mà bạn thiết lập.

## Launch Template

**Launch Template** (Khuôn mẫu khởi tạo) là một tính năng giúp bạn tạo mẫu cho việc khởi tạo các EC2 Instance. Điều này giúp tự động hóa và đơn giản hóa việc khởi tạo các EC2 Instance cho dịch vụ Auto Scaling.

## Load Balancer

**Load Balancer** (Máy cân bằng tải) là một công cụ giúp phân phối lưu lượng dữ liệu đến các tài nguyên AWS (trong trường hợp này là các EC2 Instance) trong Target Group.

## Target Group

**Target Group** (Nhóm mục tiêu) là một nhóm các tài nguyên AWS sẽ nhận lưu lượng dữ liệu được phân phối và chuyển tiếp bởi Load Balancer.

Trong bài thực hành này, chúng ta sẽ thực hiện triển khai ứng dụng bằng Auto Scaling Group để đảm bảo khả năng mở rộng linh hoạt theo nhu cầu của người dùng. Đồng thời, chúng ta cũng sẽ triển khai Load Balancer để cân bằng tải và phân phối yêu cầu truy cập từ phía người dùng đến Application Tier của chúng ta.

Hãy đảm bảo bạn đã tham khảo tài liệu Triển khai Ứng dụng FCJ Management trên Máy ảo Windows/AmazonLinux và đã nắm vững cách triển khai ứng dụng trên máy ảo. Chúng ta sẽ cần sử dụng máy ảo **FCJ Management** đã triển khai để thực hiện việc triển khai đồng loạt và mở rộng trong Auto Scaling Group.

![Auto Scaling Group](/images/2-Prerequiste/0.png?featherlight=false&width=50pc)

