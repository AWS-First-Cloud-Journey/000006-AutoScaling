---
title: "Setup network infrastructure"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>2.1. </strong>"
---

#### Create VPC

Go to the [AWS Management Console](https://aws.amazon.com/premiumsupport/knowledge-center/sign-in-console/)

- Find **VPC**
- Select **VPC**

![Image](/images/2-preparation/2.1-network/2.1.1.png?featherlight=false&width=90pc)

In the **VPC** Console

- Click **Create VPC**

![Image](/images/2-preparation/2.1-network/2.1.2.png?featherlight=false&width=90pc)

In the **Create VPC** interface

- Select **VPC and more**
- Next, type your VPC name. In this lab, we name it **`AutoScaling-Lab`**
- **IPv4 CIDR block**, type **`10.0.0.0/16`**

![Image](/images/2-preparation/2.1-network/2.1.3.png?featherlight=false&width=90pc)

Select as follows:

- Number of AZs: **3**
- Number of public subnets: **3**
- Number of private subnets: **3**
- NAT gateways: **None**

![Image](/images/2-preparation/2.1-network/2.1.4.png?featherlight=false&width=90pc)

Select as follows:

- VPC endpoints: **None**
- Choose **Create VPC**

![Image](/images/2-preparation/2.1-network/2.1.5.png?featherlight=false&width=90pc)

#### Allocate a public IP.

Allocate a public IP.

- Select **Subnets**
- Select **public subnet**
- Select **Edit subnet settings**

![Image](/images/2-preparation/2.1-network/2.1.6.png?featherlight=false&width=90pc)

Select **Enable auto-assign public IPv4 address**. Then select **Save**

![Image](/images/2-preparation/2.1-network/2.1.7.png?featherlight=false&width=90pc)

Check if the allocation was successful.

![Image](/images/2-preparation/2.1-network/2.1.8.png?featherlight=false&width=90pc)

Allocate for the remaining public subnet (do the same).

Next, we will create a **Security group**. - In the VPC console, select **Security groups** - Click **Create security group**

![Image](/images/2-preparation/2.1-network/2.1.9.png?featherlight=false&width=90pc)

Configure the **Security Group** - **Security group name**, enter **`FCJ-Management-SG`** - **Description**, enter **`Security Group for FCJ Management`** - **VPC**,select the VPC you just created: **AutoScaling-Lab**.

![Image](/images/2-preparation/2.1-network/2.1.10.png?featherlight=false&width=90pc)

Configure the **Inbound rules** - First, configure **SSH** on port **22** with **Source: MyIP** to allow access to the instance. - Next, allow **HTTP** on port **80**. - Add **Custom TCP** on port **5000** for **FCJ Management** - Finally, allow **HTTPS** on port **443**.

![Image](/images/2-preparation/2.1-network/2.1.11.png?featherlight=false&width=90pc)

Check the **Outbound rules** and click **Create security group**

![Image](/images/2-preparation/2.1-network/2.1.12.png?featherlight=false&width=90pc)

#### Create a security group for the database instance.

We create a security group for the database instance. To ensure security, we do not configure the application's security group.

Configure the **security group**

- **Security Group name**, enter **`FCJ-Mangement-DB-SG`**
- **Description**, enter **`Security Group for DB instance`**
- Select the VPC you just created.

Configure the **Inbound rules**

- Select **Add rule**
- Choose **MYSQL/Aurora** on port **3306**
- Then select the source as **FCJ-Management-SG**

![Image](/images/2-preparation/2.1-network/2.1.13.png?featherlight=false&width=90pc)

Check the **Outbound Rules** and finally click on **Create Security Group**.

![Image](/images/2-preparation/2.1-network/2.1.14.png?featherlight=false&width=90pc)
