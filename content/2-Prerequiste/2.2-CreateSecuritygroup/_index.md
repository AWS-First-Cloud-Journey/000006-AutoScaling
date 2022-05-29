---
title : "Create Security Group"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Create Security Group for FCJ Management

1. We will create a Security group for the application.

-In the VPC interface, select **Security Group**
- Select **Create security group**

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0001-createsg.png?featherlight=false&width=90pc)

2. Perform Security Group configuration

- **Security group name**, enter **```FCJ-Management-SG```**
- **Description**, enter **```Security Group for FCJ Management```**
- **VPC**, select **asg-vpc** just created.

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0002-createsg.png?featherlight=false&width=90pc)

3. Configure **Inbound rules**

- You must first configure **SSH** port 22 and **Source: MyIP** to be able to access the instance.
- Next is **HTTP** port 80.
- **Custom TCP** port **5000** for **FCJ Management**
- HTTPS port 443.

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0003-createsg.png?featherlight=false&width=90pc)


4. Check **Outbound rules** and select **Create security group**

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0004-createsg.png?featherlight=false&width=90pc)

5. Finish creating **Security Group** for the FCJ Management application. Check Security Group details.

![Create SG](/images/2-Prerequiste/2.2-CreateSecuritygroup/0005-createsg.png?featherlight=false&width=90pc)