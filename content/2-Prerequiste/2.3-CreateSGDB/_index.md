---
title : "Create Security Group DB"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---


#### Create a Security Group for the Database Instance

1. Create a Security Group for the Database instance. To ensure security, avoid configuring the application's Security Group together.

   - Select **Security Group**
   - Select **Create security group**

![Create SG](/images/3/0001.png?featherlight=false&width=90pc)

2. Configure the Security Group settings:

   - **Security Group name:** Enter **```FCJ-Management-DB-SG```**
   - **Description:** Enter ```Security Group for DB instance```
   - Select the newly created VPC

![Create SG](/images/3/0002.png?featherlight=false&width=90pc)

3. Set up **Inbound rules**:

   - Select **Add rule**
   - Select **MYSQL/Aurora** port 3306
   - Set Source as **FCJ-Management-SG**
   - Select **Create security group**

![Create SG](/images/3/0003.png?featherlight=false&width=90pc)

![Create SG](/images/3/0004.png?featherlight=false&width=90pc)

4. Complete the creation of the **Security Group** for the database.

![Create SG](/images/3/0005.png?featherlight=false&width=90pc)
