---
title: "Tạo Load Balancer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>4.2. </strong>"
---

#### Tạo Application Load Balancer

**ℹ️ Information**: Application Load Balancer (ALB) là một dịch vụ cân bằng tải thông minh hoạt động ở tầng ứng dụng (Layer 7), cho phép định tuyến lưu lượng truy cập dựa trên nội dung yêu cầu và hỗ trợ nhiều tính năng nâng cao như path-based routing và host-based routing.

Ở giao diện quản lý EC2, ở bảng điều hướng bên trái:

- Chọn **Load Balancers**
- Nhấn vào nút **Create Load Balancer**

![4.2.1](/images/4-setup-load-balancer/4.2.1.png)

Xuất hiện bảng Compare and select load balancer type:

- Ở phần Load balancer types:
  - Tại phần **Application Load Balancer**
  - Chọn **Create**

![4.2.2](/images/4-setup-load-balancer/4.2.2.png)

**💡 Pro Tip**: Application Load Balancer là lựa chọn tối ưu cho các ứng dụng web hiện đại, đặc biệt là các ứng dụng microservices hoặc container-based, vì khả năng định tuyến thông minh và hỗ trợ WebSocket.

Trong bảng Create Application Load Balancer:

- Ở phần **Basic configuration**:
  - Load balancer name: `FCJ-Management-LB`
  - Scheme: **Internet-facing**
  - Load balancer IP address type: **IPv4**

![4.2.2](/images/4-setup-load-balancer/4.2.3.png)

- Ở phần **Network mapping**:
  - VPC: **AutoScaling-Lab**
  - Subnet: Chọn Public Subnet ở **ap-southeast-1a**, **ap-southeast-1b**, và **ap-southeast-1c**

![4.2.4](/images/4-setup-load-balancer/4.2.4.png)

**⚠️ Warning**: Đảm bảo chọn đúng public subnet cho Internet-facing Load Balancer. Việc chọn private subnet sẽ khiến Load Balancer không thể tiếp nhận lưu lượng từ internet.

- Ở phần **Security groups**:
  - Chọn **FCJ-Management-SG**
- Ở phần **Listeners and routing**:
  - Default action: **FCJ-Management-TG**

![4.2.5](/images/4-setup-load-balancer/4.2.5.png)

**🔒 Security Note**: Security group cho Load Balancer nên chỉ cho phép lưu lượng HTTP/HTTPS từ internet, trong khi security group cho EC2 instance nên chỉ cho phép lưu lượng từ Load Balancer, tạo thành một kiến trúc bảo mật nhiều lớp.

- Ở phần **Summary**, kiểm tra lại các thông tin đã cấu hình cho Load Balancer
  - Nhấn vào nút **Create Load Balancer**

![4.2.6](/images/4-setup-load-balancer/4.2.6.png)

#### Xác nhận và kiểm tra Load Balancer

Sau khi tạo Load Balancer, chọn **FCJ-Management-LB** để xem thông tin chi tiết:

![4.2.7](/images/4-setup-load-balancer/4.2.7.png)

**ℹ️ Information**: Sau khi tạo, Load Balancer sẽ cần vài phút để chuyển sang trạng thái "active". Trong thời gian này, AWS đang cấp phát và cấu hình các tài nguyên cần thiết cho Load Balancer của bạn.

- Trong phần quản lý Load Balancer đã tạo:
  - Chọn **Resource map - new** để xem tổng quan liên kết của Load Balancer

![4.2.8](/images/4-setup-load-balancer/4.2.8.png)

**💡 Pro Tip**: Sử dụng DNS name của Load Balancer (hiển thị trong tab Description) để truy cập ứng dụng của bạn. Không nên sử dụng địa chỉ IP trực tiếp vì AWS có thể thay đổi địa chỉ IP của Load Balancer theo thời gian.

#### Kiểm tra hoạt động của Load Balancer

Để kiểm tra xem Load Balancer đã hoạt động chính xác hay chưa, hãy truy cập vào DNS name của Load Balancer:

1. Sao chép DNS name từ tab **Description** của Load Balancer
2. Mở trình duyệt web và dán DNS name vào thanh địa chỉ

![4.2.9](/images/4-setup-load-balancer/4.2.9.png)

**⚠️ Warning**: Nếu bạn không thể truy cập ứng dụng thông qua Load Balancer, hãy kiểm tra các điểm sau:
- Trạng thái của các EC2 instance trong Target Group (phải là "healthy")
- Cấu hình Security Group của Load Balancer và EC2 instance
- Health check đã được cấu hình đúng trong Target Group

#### Hiểu về cách hoạt động của Application Load Balancer

Application Load Balancer (ALB) hoạt động ở tầng 7 (Application Layer) của mô hình OSI, cho phép nó hiểu và xử lý các yêu cầu HTTP/HTTPS. Dưới đây là quy trình hoạt động cơ bản:

1. **Tiếp nhận yêu cầu**: ALB nhận các yêu cầu HTTP/HTTPS từ người dùng.
2. **Đánh giá quy tắc**: ALB đánh giá các quy tắc listener để xác định cách xử lý yêu cầu.
3. **Định tuyến**: Dựa trên quy tắc, ALB định tuyến yêu cầu đến target phù hợp trong Target Group.
4. **Phân phối tải**: ALB sử dụng thuật toán round robin để phân phối yêu cầu đến các target khỏe mạnh.
5. **Duy trì phiên**: Nếu được cấu hình, ALB có thể duy trì phiên người dùng với cùng một target.

**💡 Pro Tip**: ALB hỗ trợ path-based routing, cho phép bạn định tuyến các yêu cầu đến các dịch vụ backend khác nhau dựa trên URL path. Ví dụ: `/api/*` có thể được định tuyến đến API servers, trong khi `/static/*` có thể được định tuyến đến content delivery servers.

#### Lợi ích của việc sử dụng Application Load Balancer

1. **Định tuyến nâng cao**: ALB hỗ trợ định tuyến dựa trên path, host, HTTP header, và query string.
2. **Hỗ trợ WebSocket**: ALB hỗ trợ giao thức WebSocket cho các ứng dụng real-time.
3. **Hỗ trợ HTTP/2**: Cải thiện hiệu suất thông qua việc hỗ trợ HTTP/2.
4. **Tích hợp với AWS WAF**: Bảo vệ ứng dụng khỏi các cuộc tấn công web phổ biến.
5. **Sticky Sessions**: Duy trì phiên người dùng với cùng một target.
6. **Xác thực người dùng**: Tích hợp với Amazon Cognito để xác thực người dùng trước khi định tuyến yêu cầu.

**🔒 Security Note**: Để tăng cường bảo mật, bạn nên cấu hình HTTPS cho Load Balancer bằng cách sử dụng AWS Certificate Manager (ACM) để cung cấp và quản lý SSL/TLS certificates.

#### Giám sát Load Balancer

AWS cung cấp nhiều công cụ để giám sát hiệu suất của Load Balancer:

1. **CloudWatch Metrics**: Theo dõi các chỉ số như RequestCount, TargetResponseTime, và HTTPCode_ELB_5XX_Count.
2. **Access Logs**: Ghi lại thông tin chi tiết về các yêu cầu được gửi đến Load Balancer.
3. **Request Tracing**: Theo dõi các yêu cầu khi chúng đi qua Load Balancer đến các target.

**💡 Pro Tip**: Thiết lập CloudWatch Alarms để nhận thông báo khi các chỉ số hiệu suất vượt quá ngưỡng bạn đã xác định, giúp bạn phát hiện và giải quyết vấn đề trước khi chúng ảnh hưởng đến người dùng.

#### Kết luận

Chúng ta đã hoàn thành việc thiết lập Application Load Balancer cho ứng dụng FCJ-Management. Load Balancer này sẽ phân phối lưu lượng truy cập đến các EC2 instance trong Target Group, đảm bảo tính sẵn sàng cao và khả năng mở rộng cho ứng dụng của chúng ta.

Trong phần tiếp theo, chúng ta sẽ tích hợp Load Balancer này với Auto Scaling Group để tạo một hệ thống hoàn chỉnh, có khả năng tự động mở rộng và thu hẹp dựa trên nhu cầu thực tế.
