---
title : "Create Security Group DB"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---


#### Create a security group for the Database instance.


1. We create a Security group for the Database instance. To ensure security, do not configure the application's Security group together.

- Select **Security Group**
- Select **Create security group**

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0001-createsgdb.png?featherlight=false&width=90pc)

2. Practice configuration **security group**

- **Security Group name**, enter **```FCJ-Mangement-DB-SG```**
- **Description**, enter ```Security Group for DB instance```
- Select the newly created vpc

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0002-createsgdb.png?featherlight=false&width=90pc)

3. Configure **Inbound rules**

- Select **Add rule**
- Select **MYSQL/Aurora** port 3306
- Then select Soure as **FCJ-Management-SG**
- Select **Create security group**

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0003-createsgdb.png?featherlight=false&width=90pc)

4. Finish creating **Security group** for the database.

![Create SG](/images/2-Prerequiste/2.3-CreateSGDB/0004-createsgdb.png?featherlight=false&width=90pc)