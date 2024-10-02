---
title: "Create Load Balancer"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>4.2. </strong>"
---

#### Create Load Balancer

In the EC2 management interface, in the left selection panel:

- Select **Load Balancers**
- Click the **Create Load Balancer** button

![4.2.1](/images/4-setup-load-balancer/4.2.1.png)

A "Compare and select load balancer type" panel appears.

- In the Load balancer types section:
  - Under **Application Load Balancer**
  - Click **Create**

![4.2.2](/images/4-setup-load-balancer/4.2.2.png)

You will see the "Create Application Load Balancer" panel.

- In the **Basic configuration** section:
  - Load balancer name: `FCJ-Management-LB`
  - Scheme: **Internet-facing**
  - Load balancer IP address type: **IPv4**

![4.2.3](/images/4-setup-load-balancer/4.2.3.png)

- In the Network mapping section:
  - Select VPC: **AutoScaling-Lab**
  - Choose Public Subnets: **ap-southeast-1a**, **ap-southeast-1b**, **ap-southeast-1c**. Note: choose **public subnet**

![4.2.4](/images/4-setup-load-balancer/4.2.4.png)

- In the Security groups section:
  - Security groups: **FCJ-Management-SG**
- In the Listeners and routing section:
  - Default action: **FCJ-Management-TG**

![4.2.5](/images/4-setup-load-balancer/4.2.5.png)

- In the Summary section, you can review the information configured for the Load Balancer:
  - Click the **Create Balancer** button

![4.2.6](/images/4-setup-load-balancer/4.2.6.png)

#### Result

After creating the Load Balancer, select **FCJ-Management-LB** to view its information.

![4.2.7](/images/4-setup-load-balancer/4.2.7.png)

- In the management section for the created Load Balancer:
  - Select **Resource map - new** to view an overview of the Load Balancer's connections

![4.2.8](/images/4-setup-load-balancer/4.2.8.png)
