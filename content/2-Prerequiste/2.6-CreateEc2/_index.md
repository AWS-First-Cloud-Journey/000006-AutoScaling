---
title : "Create EC2 instance"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 2.6 </b> "
---


#### Create EC2 instance

1. Go to the [AWS Management Console](https://aws.amazon.com/console/)

- Find **EC2**
- Select **EC2**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0001-createec2.png?featherlight=false&width=90pc)

2. In the **EC2** interface

- Select **Instances**
- Select **Launch instances**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0002-createec2.png?featherlight=false&width=90pc)

3. Name instance, enter **```FCJ-Management```**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0003-createec2.png?featherlight=false&width=90pc)

4. Made for **AMI**

- Select **Quick Start**

- Select **Amazon Linux**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0004-createec2.png?featherlight=false&width=90pc)

5. Select **Instance type**

- Select **t2.micro**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0005-createec2.png?featherlight=false&width=90pc)

6. Configure **Network**

- **VPC**, select **asg-vpc**
- **Subnet**, select **Public subnet**
- Check if **Auto-assign public IP**?. If you haven't reviewed the public IP allocation step in the VPC creation step.

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0006-createec2.png?featherlight=false&width=90pc)

7. Select **Launch instance**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0007-createec2.png?featherlight=false&width=90pc)

8. Successfully initialized instance and select **View all instances**

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0008-createec2.png?featherlight=false&width=90pc)

9. View instance details and note **Public IPv4 address** to make the connection in the next step.

![Create EC2 instance](/images/2-Prerequiste/2.6-CreateEc2/0009-createec2.png?featherlight=false&width=90pc)