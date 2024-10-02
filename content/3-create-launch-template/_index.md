---
title: "Create Launch Template"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>3. </strong>"
---

### AMIs and Launch Template

AMIs (Amazon Machine Images) store information such as the operating system, applications, and settings in the EC2 instance from which they are created. Creating an AMI ensures that when new servers are launched, they are identical and can operate immediately.

A launch template is a tool we use to configure the initialization of new EC2 instances through attached AMIs, instance types, network configurations, and security options. When we want to launch one or more identical servers, we simply use the configured launch template to do so.

### Setting Up Launch Templates

#### Creating Amazon Machine Images (AMIs) from EC2

In the **EC2** management interface, on the right selection panel:

- Select **Instances**
- Select the **FCJ-Management** instance
- Click on **Actions**
- Choose **Image and templates**
- Click **Create image**

![3.1](/images/3-create-launch-template/3.1.png)

In the configuration panel for **Create AMI**, fill in the following information:

- **Image name**: `FCJ-Management-AMI`
- **Image description**: `AMI for FCJ-Management`
- Click **Create Image**

![3.2](/images/3-create-launch-template/3.2.png)

After creating the AMI, we will check the newly created AMI:

- Select **AMIs** to see the newly created AMI
- Click on **FCJ-Management-AMI**

![3.3](/images/3-create-launch-template/3.3.png)

{{% notice note %}}
The AMI initialization process will take about 3 minutes; after this period, we will see the **Status** of the AMI change to **Available**.
{{% /notice %}}

![3.4](/images/3-create-launch-template/3.4.png)

We have successfully created an image to save the EC2 configuration.

#### Creating Launch Templates

In the **EC2** management interface, on the right selection panel:

- Select **Launch Templates**
- Click on **Create launch template**

![3.5](/images/3-create-launch-template/3.5.png)

In the **Create launch template** panel, fill in the following information:

- In the **Launch template name and description**:
  - **Launch template name**: `FCJ-Management-template`
  - **Template version description**: `Template for FCJ Management`

![3.6](/images/3-create-launch-template/3.6.png)

- In the **Application and OS Image (Amazon Machine Image)**:
  - Select **My AMIs**
  - Choose **Owned by me**
  - Select the **Amazon Machine Image (AMI)** type and choose the created AMI **FCJ-Management-AMI**

![3.7](/images/3-create-launch-template/3.7.png)

- In the **Instance type**:
  - Choose instance type **t2.micro**
- In the **Key pair (logic)**:
  - Select the key pair named **fcj-key**

![3.8](/images/3-create-launch-template/3.8.png)

- In the **Network settings**:
  - Choose the public subnet **AutoScaling-Lab-public-ap-southeast-1a**
  - Select **Select existing security group**
  - Choose the security group **FCJ-Management-SG**
  - Finally, click **Create launch template**

![3.9](/images/3-create-launch-template/3.9.png)

#### Result

Check the newly created Launch Template:

- Select **FCJ-Management-template**

![3.10](/images/3-create-launch-template/3.10.png)

- Here, we can review the configuration of the Launch Template we created.

![3.11](/images/3-create-launch-template/3.11.png)

We have just completed creating the launch template.
