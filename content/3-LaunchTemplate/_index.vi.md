---
title : "Khởi tạo Launch Template"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.  </b> "
---

#### Khởi tạo Launch Template

Ở phần này, bạn sẽ tạo một Launch Template sử dụng AMI bạn đã tạo từ Amazon Linux 2 Instance ở bước trước.

1. Truy cập vào **EC2**

- Chọn **Launch Templates**
- Chọn **Create launch template**

![Deploy app](/images/3-LaunchTemplate/0001-launchtemplate.png?featherlight=false&width=90pc)

2. Trong giao diện **Create launch template**

- **Launch template name**, nhập **```FCJ-Management-template```**
- **Template version description**, nhập **```Template for FCJ Management```**

![Deploy app](/images/3-LaunchTemplate/0002-launchtemplate.png?featherlight=false&width=90pc)

3. Thực hiện chọn **AMI**

- Chọn **My AMIs**
- Chọn **Owned by me**
- Chọn **FCJ-Management-AMI**

![Deploy app](/images/3-LaunchTemplate/0003-launchtemplate.png?featherlight=false&width=90pc)

4. Thực hiện chọn **Instance type**

- Chọn **t2.micro**
- **Key pair**, chọn **asg-keypair** đã tạo lúc tạo **EC2** instance.

![Deploy app](/images/3-LaunchTemplate/0004-launchtemplate.png?featherlight=false&width=90pc)

5. Thực hiện cấu hình **Network**

- **Subnet**, chọn **public subnet**
- **Firewall ( Security Group)**, chọn **Select existing security group**
- Chọn **FCJ-Management-SG**

![Deploy app](/images/3-LaunchTemplate/0005-launchtemplate.png?featherlight=false&width=90pc)

6. Kiểm tra lại và thực hiện **Create launch template**

![Deploy app](/images/3-LaunchTemplate/0006-launchtemplate.png?featherlight=false&width=90pc)

7. Thực hiện thành công và chọn **View launch templates**

![Deploy app](/images/3-LaunchTemplate/0007-launchtemplate.png?featherlight=false&width=90pc)

8. Xem template vừa khởi tạo.

![Deploy app](/images/3-LaunchTemplate/0008-launchtemplate.png?featherlight=false&width=90pc)