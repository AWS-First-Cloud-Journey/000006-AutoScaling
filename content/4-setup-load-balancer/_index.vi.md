---
title: "Thiết lập Load Balancer"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: "<strong>4. </strong>"
---

#### Elastic Load Balancing (ELB)

**ℹ️ Information**: Elastic Load Balancing (ELB) là một dịch vụ AWS quan trọng để đảm bảo tính khả dụng cao và khả năng mở rộng cho ứng dụng của bạn. ELB tự động phân phối lưu lượng truy cập đến trên nhiều mục tiêu, như các phiên bản Amazon EC2, container, địa chỉ IP, và các hàm Lambda, giúp tối ưu hóa việc sử dụng tài nguyên, cải thiện hiệu suất và đảm bảo khả năng chịu lỗi.

**💡 Pro Tip**: Sử dụng ELB kết hợp với Auto Scaling Groups để tự động điều chỉnh số lượng máy chủ dựa trên nhu cầu thực tế, giúp tối ưu chi phí vận hành.

**🔒 Security Note**: ELB hỗ trợ mã hóa SSL/TLS và tích hợp với AWS Certificate Manager để bảo vệ dữ liệu trong quá trình truyền tải.

#### Nội dung

1. [Tạo Target Group](4.1-create-target-group/)
2. [Tạo Load Balancer](4.2-create-load-balancer/)

#### Lợi ích của việc sử dụng Load Balancer

Việc sử dụng Load Balancer trong kiến trúc ứng dụng của bạn mang lại nhiều lợi ích quan trọng:

1. **Tính sẵn sàng cao (High Availability)**: Load Balancer phân phối lưu lượng truy cập đến nhiều EC2 instance chạy trong các Availability Zone khác nhau, giúp ứng dụng của bạn vẫn hoạt động ngay cả khi một AZ gặp sự cố.

2. **Khả năng mở rộng (Scalability)**: Kết hợp với Auto Scaling Group, Load Balancer cho phép ứng dụng của bạn tự động mở rộng để đáp ứng nhu cầu tăng cao và thu hẹp khi nhu cầu giảm.

3. **Kiểm tra sức khỏe (Health Checks)**: Load Balancer thường xuyên kiểm tra sức khỏe của các EC2 instance và chỉ định hướng lưu lượng đến các instance khỏe mạnh.

4. **Bảo mật (Security)**: Application Load Balancer (ALB) cung cấp các tính năng bảo mật như tích hợp với AWS WAF để bảo vệ khỏi các cuộc tấn công web phổ biến.

5. **Cân bằng tải thông minh**: ELB có thể phân phối lưu lượng dựa trên nhiều thuật toán khác nhau, đảm bảo không có instance nào bị quá tải.

#### Các loại Load Balancer trong AWS

AWS cung cấp ba loại Load Balancer chính:

1. **Application Load Balancer (ALB)**: Hoạt động ở tầng ứng dụng (Layer 7) và hỗ trợ định tuyến dựa trên nội dung, phù hợp cho các ứng dụng web.

2. **Network Load Balancer (NLB)**: Hoạt động ở tầng vận chuyển (Layer 4), xử lý hàng triệu yêu cầu mỗi giây với độ trễ cực thấp, phù hợp cho các ứng dụng yêu cầu hiệu suất cao.

3. **Classic Load Balancer (CLB)**: Phiên bản cũ hơn, hỗ trợ cả Layer 4 và Layer 7, nhưng có ít tính năng hơn so với ALB và NLB.

Trong bài lab này, chúng ta sẽ sử dụng Application Load Balancer vì nó phù hợp nhất cho ứng dụng web của chúng ta.

**⚠️ Warning**: Khi thiết lập Load Balancer, hãy đảm bảo cấu hình security group phù hợp để cho phép lưu lượng từ Load Balancer đến các EC2 instance trong Auto Scaling Group.
