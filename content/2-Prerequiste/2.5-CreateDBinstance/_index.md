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

![Create DB instance](/images/5/0001.png?featherlight=false&width=90pc)

2. In **RDS** interface

    - Select **Databases**
    - Select **Create database**

![Create DB instance](/images/5/0002.png?featherlight=false&width=90pc)

3. Choose the method to create **database**

   - Select **Standard create**

![Create DB instance](/images/5/0003.png?featherlight=false&width=90pc)

4. Configure **Engine** database

   - Select **MySQL**

![Create DB instance](/images/5/0004.png?featherlight=false&width=90pc)

5. Configure **Template**

   - Select **Production**
   - For **Availability and durability**, select **Multi-AZ DB instance**

![Create DB instance](/images/5/0005.png?featherlight=false&width=90pc)

6. Next, make detailed settings

   - **DB instance identifier**, enter **`fcj-management-db-instance`**
   - **Master user**, enter **admin**
   - **Master password**, enter your choice (in the lab, enter **`123Vodanhphai`**)
   - **Confirm password**, enter the password again.

![Create DB instance](/images/5/0006.png?featherlight=false&width=90pc)

7. Perform network configuration for db instance

   - **Network type**, select **IPv4**
   - **VPC**, select **asg-vpc** created
   - **Subnet group**, select the created subnet group.
   - **VPC security group**, Select **Choose existing**
   - **Security Group**, select **FCJ-Management-DB-SG** (to avoid confusion with web SG).

![Create DB instance](/images/5/0007.png?featherlight=false&width=90pc)

8. Initialize Database with the name **awsuer**, leave the rest to default.

![Create DB instance](/images/5/0008.png?featherlight=false&width=90pc)

> Note: In the Deletion protection option, the default value is Enable, which helps protect the database from being accidentally deleted. However, in this lab, we Disable Deletion protection for easier resource cleanup at the end of the lab.

9. Check again and select **Create database**

![Create DB instance](/images/5/0009.png?featherlight=false&width=90pc)

10. Initialize DB instance in 10 minutes. When **Status** changes to **Available**, it's done.

    - Select the **db instance** just created.

![Create DB instance](/images/5/00010.png?featherlight=false&width=90pc)

11. In the **Connectivity & security** interface

    - Store the value of **Endpoint**
    - Check port **3306**

![Create DB instance](/images/5/00011.png?featherlight=false&width=90pc)

![Create DB instance](/images/5/00012.png?featherlight=false&width=90pc)
