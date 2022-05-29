---
title : "Create DB instance"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 2.5</b> "
---

#### Create DB instance

1. Go to **AWS Management Console**

- Find **RDS**
- Select **RDS**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0001-createdbinstance.png?featherlight=false&width=90pc)

2. In the **RDS** interface

- Select **Databases**
- Select **Create database**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0002-createdbinstance.png?featherlight=false&width=90pc)

3. Choose the method to create **database**

- Select **Standard create**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0003-createdbinstance.png?featherlight=false&width=90pc)

4. Configure **Engine** database

- Select **MySQL**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0004-createdbinstance.png?featherlight=false&width=90pc)

5. Configure **Template**

- Select **Production**
- For **Availability and durability**, select **Mutil-AZ DB instance**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0005-createdbinstance.png?featherlight=false&width=90pc)

6. Next, make detailed settings

- **DB instance identifier**, enter **```fcj-management-db-instance```**
- **Master user**, enter **admin**
- **Master password**, enter your choice (in the lab, enter **```123Vodanhphai```**)
- **Confirm password**, enter the password again.

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0006-createdbinstance.png?featherlight=false&width=90pc)

7. Perform network configuration for db instance

- **Network type**, select **IPv4**
- **VPC**, select the created **asg-vpc**
- **Subnet group**, select the created subnet group.
- **VPC security group**, Select **Choose existing**
- **Security Group**, select **FCJ-Management-DB-SG** (to avoid confusion with web SG).

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0007-createdbinstance.png?featherlight=false&width=90pc)

8. Initialize the Database with the name **awsuer**, and leave the rest to default.

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0008-createdbinstance.png?featherlight=false&width=90pc)

9. Check again and select **Create database**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/0009-createdbinstance.png?featherlight=false&width=90pc)

10. Initialize DB instance in 10 minutes. When **Status** changes to **Available**, it's done.

- Select **db instance** just created.

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/00010-createdbinstance.png?featherlight=false&width=90pc)

11. In the **Connectivity & security** interface

- Store value **Endpoint**
- Check port **3306**

![Create DB instance](/images/2-Prerequiste/2.5-CreateDBinstance/00011-createdbinstance.png?featherlight=false&width=90pc)