---
title : "Kết nối EC2 instance"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 2.7 </b> "
---

## Kết nối EC2 instance

1. Sử dụng **MobaXterm** để kết nối SSH vào instance qua cổng 22.

   - Chọn **Session**
   ![Connect EC2 instance](/images/7/0001.png?featherlight=false&width=90pc)

2. Trong phần **Session settings**,

   - **Remote host**, nhập **Public IPv4 address** của instance
   - **Specify username**, nhập **ec2-user**
   - Kiểm tra port 22
   - Chọn **Advanced SSH settings**
   - Chọn **Use private key** và chọn **keypair** của instance.
   - Chọn **OK**
   
   ![Connect EC2 instance](/images/7/0002.png?featherlight=false&width=90pc)

3. Thực hiện theo hướng dẫn các hình. Kết nối EC2 instance thành công.

   ![Connect EC2 instance](/images/7/0003.png?featherlight=false&width=90pc)
   ![Connect EC2 instance](/images/7/0004.png?featherlight=false&width=90pc)
   ![Connect EC2 instance](/images/7/0005.png?featherlight=false&width=90pc)

4. Cài đặt node version manager (nvm) bằng cách nhập nội dung sau vào dòng lệnh sau:



```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

![Connect EC2 instance](/images/7/0006.png?featherlight=false&width=90pc)

5. Kích hoạt nvm bằng cách nhập nội dung sau vào dòng lệnh và Sử dụng nvm để cài đặt phiên bản mới nhất của Node.js bằng cách nhập nội dung sau vào dòng lệnh.

```
. ~/.nvm/nvm.sh
nvm install 16
```

![Connect EC2 instance](/images/7/0007.png?featherlight=false&width=90pc)

6. Kiểm tra đã cài đặt nodejs thành công

```
node -v
npm -v
```

![Connect EC2 instance](/images/7/0008.png?featherlight=false&width=90pc)
