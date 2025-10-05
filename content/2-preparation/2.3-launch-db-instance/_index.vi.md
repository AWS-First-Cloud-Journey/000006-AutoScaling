---
title: "Khởi tạo Database Instance với Amazon RDS"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>2.3. </strong>"
---

#### Tạo DB Subnet Group cho Amazon RDS

Truy cập vào **AWS Management Console**:

- Tìm **RDS**
- Chọn **Aurora and RDS**

![Image](/images/2-preparation/2.3-rds/2.3.1.png?featherlight=false&width=90pc)

Tiếp tục:

- Chọn **Subnet groups**
- Chọn **Create DB subnet group**

![Image](/images/2-preparation/2.3-rds/2.3.2.png?featherlight=false&width=90pc)

Trong giao diện **Create DB subnet group**:

- **Name**, nhập **`FCJ-Management-Subnet-Group`**
- **Description**, nhập **`Subnet Group for FCJ Management`**
- Chọn VPC đã tạo

![Image](/images/2-preparation/2.3-rds/2.3.3.png?featherlight=false&width=90pc)

**ℹ️ Information**: DB Subnet Group cho phép Amazon RDS triển khai các instance database trên nhiều Availability Zone, đảm bảo tính sẵn sàng cao và khả năng chịu lỗi cho ứng dụng của bạn.

Tiến hành cấu hình **subnet**:

- Chọn các AZ
- Chọn các Private subnet

![Image](/images/2-preparation/2.3-rds/2.3.4.png?featherlight=false&width=90pc)

Chọn **Create**

![Image](/images/2-preparation/2.3-rds/2.3.5.png?featherlight=false&width=90pc)

Thành công tạo **DB Subnet Group** với 2 AZ

![Image](/images/2-preparation/2.3-rds/2.3.6.png?featherlight=false&width=90pc)

![Image](/images/2-preparation/2.3-rds/2.3.7.png?featherlight=false&width=90pc)

#### Tạo Amazon RDS Database Instance

Truy cập vào **Amazon RDS Console**:

- Chọn **Databases**
- Chọn **Create database**

![Image](/images/2-preparation/2.3-rds/2.3.8.png?featherlight=false&width=90pc)

Chọn phương thức tạo **database**:

- Chọn **Standard create**

![Image](/images/2-preparation/2.3-rds/2.3.9.png?featherlight=false&width=90pc)

Cấu hình **Engine** database:

- Chọn **MySQL**

![Image](/images/2-preparation/2.3-rds/2.3.10.png?featherlight=false&width=90pc)

**ℹ️ Information**: Amazon RDS for MySQL cung cấp khả năng quản lý đơn giản, hiệu suất cao và khả năng mở rộng cho cơ sở dữ liệu MySQL, giúp bạn tập trung vào phát triển ứng dụng thay vì quản lý cơ sở dữ liệu.

Cấu hình **Template**:

- Chọn **Production**
- Chọn **Multi-AZ DB instance**

![Image](/images/2-preparation/2.3-rds/2.3.11.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Triển khai Multi-AZ giúp tăng tính sẵn sàng bằng cách tự động tạo và duy trì một bản sao chờ đồng bộ trong một AZ khác. Trong trường hợp bảo trì theo lịch hoặc sự cố AZ, Amazon RDS sẽ tự động chuyển đổi sang bản sao chờ.

Tiếp theo, thực hiện cài đặt chi tiết:

- **DB instance identifier**, nhập **`fcj-management-db-instance`**
- **Master username**, nhập **`admin`**
- Chọn sang **Self managed**

![Image](/images/2-preparation/2.3-rds/2.3.12.png?featherlight=false&width=90pc)

Tiếp tục:
- **Master password**, nhập tùy ý của bạn (trong bài lab, nhập **`123Vodanhphai`**)
- **Confirm password**, nhập lại password một lần nữa

![Image](/images/2-preparation/2.3-rds/2.3.13.png?featherlight=false&width=90pc)

**🔒 Security Note**: Đảm bảo sử dụng mật khẩu mạnh cho cơ sở dữ liệu trong môi trường sản xuất thực tế. Mật khẩu nên bao gồm ít nhất 8 ký tự với sự kết hợp của chữ hoa, chữ thường, số và ký tự đặc biệt.

Cấu hình chi tiết cho instance:

- Chọn **`db.m5d.large`**
- Chọn **`General Purpose SSD (gp3)`**
- Allocated storage nhập vào **`20`** GB

![Image](/images/2-preparation/2.3-rds/2.3.14.png?featherlight=false&width=90pc)

Thực hiện cấu hình Connectivity cho DB instance:

- Chọn **Don't connect to an EC2 compute resource**
- **VPC**, chọn **`AutoScaling-Lab`** đã tạo
- **Subnet group**, chọn subnet group đã tạo

![Image](/images/2-preparation/2.3-rds/2.3.15.png?featherlight=false&width=90pc)

Tiếp tục:

- **VPC security group**, Chọn **Choose existing**
- **Security Group**, chọn **FCJ-Management-DB-SG** (tránh nhầm lẫn với SG của web)

![Image](/images/2-preparation/2.3-rds/2.3.16.png?featherlight=false&width=90pc)

**⚠️ Warning**: Đảm bảo rằng Security Group cho RDS chỉ cho phép kết nối từ các EC2 instance trong Auto Scaling Group của bạn. Không mở cổng database ra internet công cộng để tránh các rủi ro bảo mật.

Khởi tạo Initial Database với tên **`awsfcjuer`**, còn lại để mặc định.

![Image](/images/2-preparation/2.3-rds/2.3.17.png?featherlight=false&width=90pc)

Bấm **Create database**

![Image](/images/2-preparation/2.3-rds/2.3.18.png?featherlight=false&width=90pc)

Database instance đã được tạo thành công.

![Image](/images/2-preparation/2.3-rds/2.3.19.png?featherlight=false&width=90pc)

**ℹ️ Information**: Quá trình tạo Amazon RDS Database Instance có thể mất từ 5-10 phút. Trong thời gian này, AWS đang cấp phát tài nguyên, thiết lập cấu hình và triển khai cơ sở dữ liệu của bạn.

Chúng ta có được **Endpoint** và **Port** như dưới đây.

![Image](/images/2-preparation/2.3-rds/2.3.20.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Lưu lại thông tin Endpoint và Port này để sử dụng trong các bước tiếp theo khi cấu hình kết nối từ ứng dụng FCJ Management đến cơ sở dữ liệu. Endpoint này sẽ không thay đổi ngay cả khi RDS instance được khởi động lại.
#### Tổng kết

Trong phần này, chúng ta đã hoàn thành việc khởi tạo và cấu hình Amazon RDS Database Instance cho ứng dụng FCJ Management. Các bước chính bao gồm:

1. **Tạo DB Subnet Group**: Phân bổ cơ sở dữ liệu trên nhiều Availability Zone để đảm bảo tính sẵn sàng cao
2. **Cấu hình DB Instance**: Lựa chọn loại database, phiên bản, và cấu hình phù hợp
3. **Thiết lập bảo mật**: Áp dụng Security Group chuyên biệt để kiểm soát truy cập
4. **Khởi tạo cơ sở dữ liệu**: Tạo database ban đầu để sử dụng cho ứng dụng

**🔒 Security Note**: Amazon RDS cung cấp nhiều tính năng bảo mật như mã hóa dữ liệu, sao lưu tự động, và cập nhật bảo mật. Trong môi trường sản xuất, bạn nên bật tính năng mã hóa dữ liệu và thiết lập lịch sao lưu phù hợp với yêu cầu khôi phục dữ liệu của ứng dụng.

**💡 Pro Tip**: Để tối ưu chi phí và hiệu suất, bạn có thể sử dụng Amazon RDS Performance Insights để giám sát và điều chỉnh hiệu suất database mà không cần kiến thức chuyên sâu về quản trị cơ sở dữ liệu.

Trong bước tiếp theo, chúng ta sẽ tiến hành cài đặt dữ liệu cho database để chuẩn bị cho việc triển khai ứng dụng FCJ Management.
