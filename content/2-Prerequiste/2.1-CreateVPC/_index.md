---
title : "Create VPC"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

#### Create VPC


1. Go to [AWS Management Console](https://aws.amazon.com/premiumsupport/knowledge-center/sign-in-console/)

- Find **VPC**
- Select **VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0001-createvpc.png?featherlight=false&width=90pc)

2. In the **VPC** interface

- Select **Your VPCs**
- Select **Create VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0002-createvpc.png?featherlight=false&width=90pc)

3. In the **Create VPC** interface

- Select **VPC, subnets, etc,**
- **Name**, enter **```asg```**
- **IPv4 CIDR block**, enter **10.0.0.0/16**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0003-createvpc.png?featherlight=false&width=90pc)

4. Select **Create VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0004-createvpc.png?featherlight=false&width=90pc)

5. Create VPC successfully and select **View VPC**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0005-createvpc.png?featherlight=false&width=90pc)

6. Details of the newly created VPC.

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0006-createvpc.png?featherlight=false&width=90pc)

7. Implement public IP allocation.

- Select **Subnets**
- Select **public subnet**
- Select **Edit subnet settings**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0007-createvpc.png?featherlight=false&width=90pc)

8. Select **Enable auto-assign public IPv4 address**

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0008-createvpc.png?featherlight=false&width=90pc)

9. Check that the allocation was successful.

![Create VPC](/images/2-Prerequiste/2.1-CreateVPC/0009-createvpc.png?featherlight=false&width=90pc)

10. Allocate the remaining Public subnet (do the same).