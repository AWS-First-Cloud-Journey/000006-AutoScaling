---
title : "Các bước chuẩn bị"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

#### Các bước chuẩn bị

Trong bài thực hành này, chúng ta cần chuẩn bị một số dịch vụ để có thể tiến hành triển khai ứng dụng FCJ Management sử dụng Auto Scaling Group cùng với Elastic Load Balancer. Một cách tổng quan, chúng ta sẽ triển khai ứng dụng FCJ Management theo kiến trúc như sau:

![Create VPC](/images/2-Prerequiste/0.png?featherlight=false&width=55pc)

#### Nội dung 

1. [Tạo VPC](2.1-createvpc/)
2. [Tạo Security Group cho FCJ Management instance](2.2-createsecuritygroup/)
3. [Tạo Security Group cho DB instance](2.3-createsgdb/)
4. [Tạo DB Subnet Group](2.4-createdbsubnetgroup/)
5. [Tạo DB instance](2.5-createdbinstance/)
6. [Tạo EC2 instance](2.6-createec2/)
7. [Kết nối EC2 instance](2.7-connectec2/)
8. [Kết nối DB instance](2.8-connectdbinstance/)
9. [Triển khai ứng dụng](2.9-deployapp/)
10. [Khởi tạo AMI từ máy ảo](2.10-createami/)
