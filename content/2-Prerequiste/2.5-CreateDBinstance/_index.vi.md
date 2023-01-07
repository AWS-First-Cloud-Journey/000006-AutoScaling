---
title : "Tạo DB instance"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 2.5</b> "
---

#### Tạo DB instance

1. Truy cập vào **AWS Management Console**

   - Tìm **RDS**
   - Chọn **RDS**

![Create DB instance](/images/5/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **RDS**

    - Chọn  **Databases**
    - CHọn **Create database**

![Create DB instance](/images/5/0002.png?featherlight=false&width=90pc)

3. Chọn phương thức tạo **database**

   - Chọn **Standard create**

![Create DB instance](/images/5/0003.png?featherlight=false&width=90pc)

4. Cấu hình **Engine** database

   - Chọn **MySQL**

![Create DB instance](/images/5/0004.png?featherlight=false&width=90pc)

5. Cấu hình **Template**

   - Chọn **Dev/Test**
   - Đối với **Availability and durability**, chọn **Mutil-AZ DB  instance**

![Create DB instance](/images/5/0005.png?featherlight=false&width=90pc)

6. Tiếp theo, thực hiện cài đặt chi tiết

   - **DB instance identifier**, nhập **```fcj-management-db-instance```**
   - **Master user**, nhập **admin** 
   - **Master password**, nhập tùy ý của bạn ( trong bài lab, nhập **```123Vodanhphai```**)
   - **Confirm password**, nhập lại password 1 lần nữa.

![Create DB instance](/images/5/0006.png?featherlight=false&width=90pc)

7. Thực hiện cấu hình network cho db instance

   - **Network type**, chọn **IPv4**
   - **VPC**, chọn **asg-vpc** đã tạo
   - **Subnet group**, chọn subnet group đã tạo.
   - **VPC security group**, Chọn **Choose existing**
   - **Security Group**, chọn **FCJ-Management-DB-SG** (tránh nhầm lẫn với SG của web).

![Create DB instance](/images/5/0007.png?featherlight=false&width=90pc)

8. Khởi tạo Database với tên **awsuer**, còn lại để mặc định.

![Create DB instance](/images/5/0008.png?featherlight=false&width=90pc)

9. Kiểm tra lại và chọn **Create database**

![Create DB instance](/images/5/0009.png?featherlight=false&width=90pc)

10. Khởi tạo DB instance trong 10 phút. Khi **Status** chuyển sang **Available** là hoàn thành.

    - Chọn vào **db instance** vừa tạo.

![Create DB instance](/images/5/00010.png?featherlight=false&width=90pc)

11. Trong giao diện **Connectivity & security**

    - Lưu trữ giá trị **Endpoint**
    - Kiểm tra port **3306**

![Create DB instance](/images/5/00011.png?featherlight=false&width=90pc)

![Create DB instance](/images/5/00012.png?featherlight=false&width=90pc)