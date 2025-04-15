---
title: "Khởi tạo EC2 Instance"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>2.2. </strong>"
---

#### Tạo EC2 Instance

Truy cập vào [AWS Management Console](https://aws.amazon.com/console/):

- Tìm **EC2**
- Chọn **EC2**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.1.png?featherlight=false&width=90pc)

Trong giao diện **EC2**:

- Chọn **Launch instances**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.2.png?featherlight=false&width=90pc)

#### Cấu hình thông tin cơ bản

Đặt tên cho instance, nhập **`FCJ-Management`**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.3.png?featherlight=false&width=90pc)

#### Chọn Amazon Machine Image (AMI)

Thực hiện chọn **AMI**:

- Chọn **Quick Start**
- Chọn **Amazon Linux**
- Chọn **Amazon Linux 2023 AMI**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.4.png?featherlight=false&width=90pc)

**ℹ️ Information**: Amazon Linux 2023 là phiên bản mới nhất của Amazon Linux, được tối ưu hóa cho workloads trên AWS với hiệu suất cao, thời gian khởi động nhanh và các tính năng bảo mật nâng cao như SELinux được kích hoạt mặc định.

#### Chọn loại instance và tạo key pair

Chọn **Instance type**:

- Chọn **t2.micro**
- Chọn **Create new key pair**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.5.png?featherlight=false&width=90pc)

Cấu hình key pair:

- Đặt tên là **`fcj-key`**
- Key pair type: **RSA**
- Private key format: **.pem**
- Bấm **Create key pair**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.6.png?featherlight=false&width=90pc)

**🔒 Security Note**: Key pair là thành phần quan trọng để bảo mật kết nối SSH đến EC2 instance. Hãy lưu trữ file .pem ở nơi an toàn, đặt quyền truy cập phù hợp (chmod 400 trên Linux/macOS) và không chia sẻ với người khác. AWS không lưu trữ private key, nên nếu bị mất, bạn sẽ cần tạo key pair mới.

#### Cấu hình mạng

Thực hiện cấu hình **Network**:

- Bấm vào nút Edit
- **VPC**, chọn VPC đã tạo.
- **Subnet**, chọn **Public subnet**
- Kiểm tra đã **Auto-assign public IP** chưa? Nếu chưa, xem lại bước cấp phát public IP ở bước tạo VPC.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.7.png?featherlight=false&width=90pc)

#### Cấu hình bảo mật và khởi tạo

Tiếp tục:

- Chọn **Select existing security group** rồi chọn **FCJ-Management-SG**.
- Chọn **Launch instance**.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.8.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Sử dụng security group đã được cấu hình sẵn giúp đảm bảo tính nhất quán trong chính sách bảo mật và dễ dàng quản lý quyền truy cập mạng. Bạn có thể áp dụng cùng một security group cho nhiều EC2 instances, giúp đơn giản hóa việc quản lý và cập nhật các quy tắc bảo mật.

#### Xác nhận khởi tạo thành công

Khởi tạo instance thành công.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.9.png?featherlight=false&width=90pc)

**ℹ️ Information**: EC2 instance sẽ mất khoảng 1-2 phút để khởi động hoàn toàn và sẵn sàng cho kết nối SSH. Bạn có thể theo dõi trạng thái của instance trong tab "Instance state" và đợi đến khi trạng thái chuyển sang "Running" và kiểm tra "Status check" đạt 2/2 checks passed.

#### Kết nối đến EC2 Instance

Sau khi EC2 instance đã được khởi tạo thành công và ở trạng thái "Running", chúng ta có thể kết nối đến instance bằng SSH.

**Đối với người dùng Windows:**

1. Tải và cài đặt PuTTY từ [trang chủ PuTTY](https://www.putty.org/) nếu bạn chưa có.
2. Sử dụng PuTTYgen để chuyển đổi file .pem thành .ppk:
   - Mở PuTTYgen
   - Chọn "Load" và tìm file fcj-key.pem đã tải về
   - Chọn "Save private key" và lưu file .ppk
3. Mở PuTTY và cấu hình:
   - Nhập địa chỉ IP Public của EC2 instance vào trường Host Name
   - Trong mục Connection > SSH > Auth, chọn Browse và tìm đến file .ppk đã tạo
   - Nhập "ec2-user" khi được yêu cầu username

**Đối với người dùng macOS/Linux:**

1. Mở Terminal
2. Đặt quyền cho file key:
   ```bash
   chmod 400 /đường/dẫn/đến/fcj-key.pem
   ```
3. Kết nối đến instance:
   ```bash
   ssh -i /đường/dẫn/đến/fcj-key.pem ec2-user@địa-chỉ-IP-Public
   ```

![Image](/images/2-preparation/2.2-launch-ec2/2.2.10.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Bạn cũng có thể sử dụng tính năng EC2 Instance Connect trên AWS Management Console để kết nối đến instance mà không cần cấu hình SSH client. Chỉ cần chọn instance và nhấp vào nút "Connect".



