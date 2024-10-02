---
title: "Launch EC2 Instance"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>2.2. </strong>"
---

Access the [AWS Management Console](https://aws.amazon.com/console/):

- Search for **EC2**
- Select **EC2**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.1.png?featherlight=false&width=90pc)

In the **EC2** console:

- Click on **Launch instances**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.2.png?featherlight=false&width=90pc)

Name the instance, enter **`FCJ-Management`**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.3.png?featherlight=false&width=90pc)

For **AMI**:

- Select **Quick Start**
- Selec **Amazon Linux**
- Select **Amazon Linux 2023 AMI**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.4.png?featherlight=false&width=90pc)

Select **Instance type**:

- Select **t2.micro**
- Click **Create new key pair**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.5.png?featherlight=false&width=90pc)

Configure the key pair

- Name it **`fcj-key`**
- Key pair type: **RSA**
- Private key format: **.pem**
- Click **Create key pair**

![Image](/images/2-preparation/2.2-launch-ec2/2.2.6.png?featherlight=false&width=90pc)

Configure the **Network**:

- Click the Edit button
- For **VPC**, select the VPC you created.
- For **Subnet**, choose **Public subnet**
- Check if **Auto-assign public IP** is enabled. If not, review the step for allocating a public IP when creating the VPC.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.7.png?featherlight=false&width=90pc) 8. Continue:

- Select **Select existing security group** and then choose **FCJ-Management-SG**.
- Click **Launch instance**.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.8.png?featherlight=false&width=90pc)

Complete the creation of the Security Group for the database.

![Image](/images/2-preparation/2.2-launch-ec2/2.2.9.png?featherlight=false&width=90pc)
