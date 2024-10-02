---
title: "Create Target Group"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>4.1. </strong>"
---

#### Create Target Group

In the EC2 management interface, on the left side panel, scroll down to the **Load Balancing** section.

- Select **Target Group**
- Click on **Create target group**

![4.1.1](/images/4-setup-load-balancer/4.1.1.png)

The **Specify group details** dialog will appear. Configure it as follows:

- In the Basic configuration section:
  - Choose a target type: **Instances**
  - Target group name: `FCJ-Management-TG`

![4.1.2](/images/4-setup-load-balancer/4.1.2.png)

- Continue in the Basic configuration section:
  - Protocol: port **HTTP**, **5000**
  - IP address: **IPv4**
  - VPC: **AutoScaling-Lab**
  - Protocol version: **HTTP1**

![4.1.3](/images/4-setup-load-balancer/4.1.3.png)

- Click **Next**

![4.1.4](/images/4-setup-load-balancer/4.1.4.png)

Next, we proceed to **Register target**.

- In the Available instance section:
  - Select target group **FCJ-Management-TG**
  - Ports for the selected instances: **5000**
  - Choose **Include as pending below**

![4.1.5](/images/4-setup-load-balancer/4.1.5.png)

- In the Review targets section:
  - You will see the target group has been registered previously
  - Click **Create target group**

![4.1.6](/images/4-setup-load-balancer/4.1.6.png)

#### Result

We have completed the creation of the Target Group. Select the Target Group **FCJ-Management-TG** that was just created to view its information.

![4.1.7](/images/4-setup-load-balancer/4.1.7.png)
