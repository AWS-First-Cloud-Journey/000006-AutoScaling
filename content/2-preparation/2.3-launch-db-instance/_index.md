---
title: "Launch a Database Instance with RDS"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>2.3. </strong>"
---

#### Create a subnet group for the database instance.

Access the AWS **AWS Management Console**

- Search for **RDS**
- Select **RDS**

![Image](/images/2-preparation/2.3-rds/2.3.1.png?featherlight=false&width=90pc)

Continue:

- Select **Subnet groups**
- Select **Create DB subnet group**

![Image](/images/2-preparation/2.3-rds/2.3.2.png?featherlight=false&width=90pc)

In the **Create DB subnet group** interface

- For **Name**, enter **`FCJ-Management-Subnet-Group`**
- For **Description**, enter **`Subnet Group for FCJ Management`**
- Select the VPC you created.

![Image](/images/2-preparation/2.3-rds/2.3.3.png?featherlight=false&width=90pc)

Configure the **subnet**

- Select the availability zones (AZs)
- Choose the private subnets.

![Image](/images/2-preparation/2.3-rds/2.3.4.png?featherlight=false&width=90pc)

Click on **Create**

![Image](/images/2-preparation/2.3-rds/2.3.5.png?featherlight=false&width=90pc)

Successfully created the **DB Subnet Group** with 2 AZs.

![Image](/images/2-preparation/2.3-rds/2.3.6.png?featherlight=false&width=90pc)

![Image](/images/2-preparation/2.3-rds/2.3.7.png?featherlight=false&width=90pc)

#### Create a database instance.

Access the **RDS AWS Management Console**

- Select **Databases**
- Click on **Create database**

![Image](/images/2-preparation/2.3-rds/2.3.8.png?featherlight=false&width=90pc)

Choose the method to create the **database**

- Select **Standard create**

![Image](/images/2-preparation/2.3-rds/2.3.9.png?featherlight=false&width=90pc)

Configure the **Engine** for the database

- Select **MySQL**

![Image](/images/2-preparation/2.3-rds/2.3.10.png?featherlight=false&width=90pc)

Configure **Template**

- Select **Production**
- Select **Mutil-AZ DB instance**

![Image](/images/2-preparation/2.3-rds/2.3.11.png?featherlight=false&width=90pc)

Next, proceed with the detailed configuration

- For **DB instance identifier**, enter **`fcj-management-db-instance`**
- For **Master username**, enter **`admin`**
- Select **Self managed**

![Image](/images/2-preparation/2.3-rds/2.3.12.png?featherlight=false&width=90pc)

Continue: - For **Master password**, enter your choice (in this lab, enter **`123Vodanhphai`**) - For **Confirm password**, re-enter the password once more.

![Image](/images/2-preparation/2.3-rds/2.3.13.png?featherlight=false&width=90pc)

Configure the details for the instance:

- Select **`db.m5d.large`**
- Select **`General Purpose SSD (gp3)`**
- For Allocated storage, enter **`20`**

![Image](/images/2-preparation/2.3-rds/2.3.14.png?featherlight=false&width=90pc)

Configure the Connectivity for the db instance

- Select **Don't connect to an EC2 compute resouce**
- For **VPC**, select the created **`AutoScaling-Lab`**
- For **Subnet group**, choose the subnet group you created.

![Image](/images/2-preparation/2.3-rds/2.3.15.png?featherlight=false&width=90pc)

Continue:

- For **VPC security group**, select **Choose existing**
- For **Security Group**, select **FCJ-Management-DB-SG** (to avoid confusion with the web application's security group).

![Image](/images/2-preparation/2.3-rds/2.3.16.png?featherlight=false&width=90pc)

Initialize the database with the name **`awsfcjuer`**, and leave the rest as default.

![Image](/images/2-preparation/2.3-rds/2.3.17.png?featherlight=false&width=90pc)

Click on **Create database**

![Image](/images/2-preparation/2.3-rds/2.3.18.png?featherlight=false&width=90pc)

The database instance has been created successfully.

![Image](/images/2-preparation/2.3-rds/2.3.19.png?featherlight=false&width=90pc)

We have the Endpoint and Port as shown below.

![Image](/images/2-preparation/2.3-rds/2.3.20.png?featherlight=false&width=90pc)
