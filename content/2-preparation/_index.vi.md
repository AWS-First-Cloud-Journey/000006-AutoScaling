---
title: "Các bước chuẩn bị"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>2. </strong>"
---

Trong bài thực hành này, chúng ta cần chuẩn bị một số dịch vụ để có thể tiến hành triển khai ứng dụng FCJ Management sử dụng Auto Scaling Group cùng với Elastic Load Balancer. Một cách tổng quan, chúng ta sẽ triển khai ứng dụng FCJ Management theo kiến trúc như sau:
![Create VPC](/images/2-preparation/diagram0006.png)

### Nội dung

1. [Thiết lập hạ tầng mạng](2.1-setup-network/)
2. [Khởi tạo EC2 instance](2.2-launch-ec2-instance/)
3. [Khởi tạo Database instance với RDS](2.3-launch-db-instance/)
4. [Cài đặt dữ liệu cho database](2.4-add-data-to-db/)
5. [Triển khai máy chủ web](2.5-deploy-web-server/)
6. [Chuẩn bị metric cho Predictive scaling](2.6-prepare-metrics-for-predictive-scaling/)
