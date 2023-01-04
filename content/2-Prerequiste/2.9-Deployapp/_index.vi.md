---
title : "Triển khai ứng dụng FCJ Management"
date :  "`r Sys.Date()`" 
weight : 9
chapter : false
pre : " <b> 2.9  </b> "
---

#### Triển khai ứng dụng FCJ Management

1. Chúng ta sử dụng git để clone source code. Trước hết, cài đặt git bằng lệnh sau:

```
sudo yum install git
```

![Deploy app](/images/9/0001.png?featherlight=false&width=90pc)

![Deploy app](/images/9/0002.png?featherlight=false&width=90pc)

2. Sử dụng lệnh git init được sử dụng để tạo, khởi tạo một kho chứa Git mới (Git Repo) ở local.

```
git init
```

![Deploy app](/images/9/0003.png?featherlight=false&width=90pc)


3. Thực hiện clone repository code ứng dụng

```
git clone https://github.com/First-Cloud-Journey/000004-EC2.git
```
![Deploy app](/images/9/0004.png?featherlight=false&width=90pc)

4. Đến thư mục của bài lab 000004-EC2

```
cd 000004-EC2
```

![Deploy app](/images/9/0004.png?featherlight=false&width=90pc)

5. NPM là viết tắt của Node package manager là một công cụ tạo và quản lý các thư viện lập trình Javascript cho Node.js. Sử dụng npm init khởi tạo project sẽ tạo ra file package.json mẫu.

```
npm init

```

- Nếu trường hợp chưa cài đặt Nodejs bạn có thể tham khảo [Cài đặt Nodejs trên Amazon Linux](https://000004.awsstudygroup.com/vi/6-awsfcjmanagement-linux/6.2-setupnodejsonec2linux/)

![Deploy app](/images/9/0005.png?featherlight=false&width=90pc)

6. Tiếp theo chúng ta thực hiện dependencies installation

   - express
   - Dotenv
   - express-handlebars
   - body-parser
   - mysqs

```
npm install express dotenv express-handlebars body-parser mysql
```

![Deploy app](/images/9/0006.png?featherlight=false&width=90pc)

![Deploy app](/images/9/0007.png?featherlight=false&width=90pc)

7. Thực hiện kiểm tra và tạo một file **.env** sử dụng **vi** để cấu hình database.


![Deploy app](/images/9/0008.png?featherlight=false&width=90pc)


![Deploy app](/images/9/0009.png?featherlight=false&width=90pc)

8. Thực hiện cấu hình database

```
DB_HOST = 'db-instance.crmmitoajvxx.us-east-1.rds.amazonaws.com'
DB_NAME = 'awsuser'
DB_USER = 'admin'
DB_PASS = '123Vodanhphai'
```

- Trong đó, DB_HOST là Enpoint của DB instance
- DB_NAME là tên database đã được tạo trong DB instance
- DB_USER là tên người dùng database đã được tạo trong DB instance
- DB_PASS là mật khẩu database đã được tạo trong DB instance

![Deploy app](/images/9/00010.png?featherlight=false&width=90pc)

9. Khởi động lại Express server. Sử dụng Nodemon để tiết kiệm thời gian

```
npm install --save-dev nodemon
```

![Deploy app](/images/9/00012.png?featherlight=false&width=90pc)

10. Khởi động local server

```
npm start
```

![Deploy app](/images/9/00013.png?featherlight=false&width=90pc)

11. Truy cập vào **EC2**

- Chọn **Instances**
- Chọn **FCJ-Management** instance
- Sao chép **Public IPv4 address**


12.  Sử dụng trình duyệt và dán **Public IPv4 address** để kiểm tra ứng dụng.   


![Deploy app](/images/9/00014.png?featherlight=false&width=90pc)