---
title: "Tạo Launch Template"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>3. </strong>"
---

### AMIs và Launch Template

AMIs (Amazon Machine Images) lưu trữ các thông tin như hệ điều hành, ứng dụng, cài đặt ở EC2 mà chúng được tạo. Việc tạo ra AMI đảm bảo rằng khi máy chủ mới được tạo ra thì nó được mọi máy chủ mới đều giống nhau và có thể hoạt động ngay lập tức

Launch template là một công cụ mà chúng ta dùng để cấu hình cho việc khởi tạo các EC2 mới thông AMI được gắn, loại instance, cấu hình mạng, và các tuỳ chọn bảo mật. Khi chúng ta muốn khởi tạo một hoặc nhiều máy chủ giống nhau, chúng ta chỉ cần sử dụng launch template đã được cấu hình để thực hiện việc này.

### Thiết lập Launch Templates

#### Tạo Amazon Machine Images (AMIs) từ EC2

Ở trong phần giao diện quản lý **EC2**, ở bảng chọn bên phải

- Chọn **Instances**
- Chọn **FCJ-Management** instance
- Chọn **Actions**
- Chọn **Image and templates**
- Ấn **Create image**

![3.1](/images/3-create-launch-template/3.1.png)

Trong bảng cấu hình cho **Create AMI**, chúng ta tiến hành điền các thông tin sau

- Image name `FCJ-Management-AMI`
- Image description `AMI for FCJ-Management`
- Ấn **Create Image**

![3.2](/images/3-create-launch-template/3.2.png)

Sau khi tạo AMI chúng ta sẽ kiểm tra AMI vừa tạo

- Chọn **AMIs** chúng ta sẽ thấy AMI vừa tạo được
- Chọn **FCJ-Management-AMI**

![3.3](/images/3-create-launch-template/3.3.png)

{{% notice note %}}
Quá trình khởi tạo AMI sẽ mất khoảng 3 phút, sau quá trình khởi tạo chúng ta sẽ thấy **Status** của AMI chuyển từ trạng **Available**
{{% /notice %}}
![3.4](/images/3-create-launch-template/3.4.png)

Chúng ta vừa hoàn thành tạo một Image để lưu cấu hình của EC2

#### Tạo Launch Templates

Ở giao diện quản lý **EC2**, ở bảng chọn bên phải

- Chọn **Launch Templates**
- Chọn **Create lkunch template**

![3.5](/images/3-create-launch-template/3.5.png)

Ở trong bảng **Create launch template** hãy điền các thông tin sau

- Ở phần **Launch template name and description**
  - Launch template name `FCJ-Management-template`
  - Template version description `Template for FCJ Management`

![3.6](/images/3-create-launch-template/3.6.png)

- Ở phần **Application and OS Image (Amazon Machine Image)**
  - Chọn **My AMIs**
  - Chọn **Owned by me**
  - Chọn loại **Amazon Machine Image (AMI)**, chọn AMI đã tạo **FCJ-Management-AMI**

![3.7](/images/3-create-launch-template/3.7.png)

- Ở phần **Instance type**
  - Chọn loại Instance **t2.micro**
- Ở phần **Key pair (logic)**
  - Chọn **Key pair name** có tên là **fcj-key**

![3.8](/images/3-create-launch-template/3.8.png)

- Ở phần **Network settings**
  - Chọn subnet public **AutoScaling-Lab-public-ap-southeast-1a**
  - Chọn **Select existing security group**
  - Chọn security group **FCJ-Management-SG**
  - Cuối cùng, chọn **Create launch template**

![3.9](/images/3-create-launch-template/3.9.png)

#### Kết quả

Kiểm tra Launch Template vừa tạo

- Chọn **FCJ-Management-template**

![3.10](/images/3-create-launch-template/3.10.png)

- Ở đây chúng ta có thể xem lại cấu hình Launch Template chúng ta đã tạo

![3.11](/images/3-create-launch-template/3.11.png)

Chúng ta vừa hoàn thành tạo Launch Template.
