---
title: "Create Auto Scaling Group"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<strong>6. </strong>"
---

### Issue in the Previous Section

In the testing results mentioned earlier, we can see that when the application receives many requests, it becomes unstable. The solution is to increase the number of EC2 Instances in the system and use a Load Balancer to distribute the requests from users.

However, this manual method is not very practical because to launch an EC2 Instance, we need to have the "core" inside it, which is the application responsible for handling those requests along with other libraries.

### Setting Up Auto Scaling Group

#### Setting Up Launch Template

In the **EC2** management console, scroll down the selection panel on the right.

- Select **Auto Scaling Groups**.
- Click **Create Auto Scaling group**.

![6.1](/images/6-create-auto-scaling-group/6.1.png)

In the **Auto Scaling group** creation interface, enter the following information:

- Name: `FCJ-Management-ASG`
- In Launch template:
  - Launch template: select `FCJ-Management-template` (or any name you choose).
  - Version: **Default (1)** as the default choice.

![6.2](/images/6-create-auto-scaling-group/6.2.png)

{{% notice note %}}
Note that the ASG name should match the name of the ASG set in section **2.6**, which is for preparing data for Predictive Scaling.
{{% /notice %}}

{{% notice note %}}
The **Launch template** selected for the ASG must be the one configured with _MySQL Client_, _Node_, _Source Code_, and _PM2_ to ensure the Targets operate normally. If you followed the steps in sections **2** and **3**, you have done it correctly.
{{% /notice %}}

![6.3](/images/6-create-auto-scaling-group/6.3.png)

#### Configuring the Network

In the Network section, select the following information:

- VPC: select **AutoScaling-Lab** VPC, which we created earlier in the tutorial.
- Availability Zones and subnets: select **3 public subnets** that we created.
- Click **Next**.

![6.4](/images/6-create-auto-scaling-group/6.4.png)

#### Configuring the Load Balancer and Other Settings

Previously, we created an **Application Load Balancer** and a **Target Group** and attached it to the Load Balancer. Now, select the following options:

- Load balancing: select **Attach to an existing load balancer**.
- Attach to an existing load balancer: choose **Choose from your load balancer target group**.
- Existing load balancer target group: select **FCJ-Management-TG | HTTP**.

![6.5](/images/6-create-auto-scaling-group/6.5.png)

{{% notice note %}}
When the Target Group and **Application Load Balancer** are correctly configured, the **Existing load balancer target group** option will show the Target Group, indicating that both ALB and TG exist.
{{% /notice %}}

In the VPC Lattice integration options: select **No VPC Lattice service**, as we are not configuring this option in this tutorial.

Next, in Health checks, select (check) **Turn on Elastic Load Balancing health checks**. Leave the remaining settings as default.

![6.6](/images/6-create-auto-scaling-group/6.6.png)

In the Additional settings section, under Monitoring:

- Select (check) **Enable group metrics collection within CloudWatch**.
- Click **Next**.

![6.7](/images/6-create-auto-scaling-group/6.7.png)

#### Setting Group Size and Scaling

In this section, define the group's scaling behavior and the number of Instances to be created during scaling, including scaling out (expanding) and scaling in (shrinking).

- In the Group size section:
  - Desired capacity: **1**
- In the Scaling section:
  - Scaling limits:
    - Min desired capacity: **1**
    - Max desired capacity: **3**

![6.8](/images/6-create-auto-scaling-group/6.8.png)

In the Automatic scaling - optional section: choose **No scaling policies** for now, as we won't configure scaling policies for the ASG yet.

![6.9](/images/6-create-auto-scaling-group/6.9.png)

In the Instance maintenance policy section: choose **No policy**.

![6.10](/images/6-create-auto-scaling-group/6.10.png)

{{% notice note %}}
We are not configuring ASG policies here because we will apply scaling strategies later, including four different strategies.
{{% /notice %}}

#### Setting Up Notifications

In this section, we'll configure email notifications (using Amazon SNS) when the ASG:

- Launches a new Instance.
- Terminates an Instance.
- Fails to launch an Instance.
- Fails to terminate an Instance.

We'll create notifications for one email address, including the following details:

- Send a notification to: `asg-topic`. Select a topic to send notifications.
- With these recipients: enter the email address where you want SNS to send notifications.
- Event types: select all.
- Click **Next**.

![6.11](/images/6-create-auto-scaling-group/6.11.png)

![6.12](/images/6-create-auto-scaling-group/6.12.png)

Review the information and click **Create Auto Scaling group**.

![6.13](/images/6-create-auto-scaling-group/6.13.png)

#### Results

During the creation process, an email will be sent, so make sure to check and confirm email notifications from the selected topic.

![6.14](/images/6-create-auto-scaling-group/6.14.png)

![6.15](/images/6-create-auto-scaling-group/6.15.png)

Since we set **Desired capacity = 1**, when the ASG is created, it will automatically launch a new Instance, and you'll receive a new email.

![6.16](/images/6-create-auto-scaling-group/6.16.png)

Check the Activity tab of the FCJ-Management-ASG to verify.

![6.17](/images/6-create-auto-scaling-group/6.17.png)

{{% notice note %}}
During the execution of other scaling strategies, you may receive many emails, so keep an eye on your inbox. This is intentional to help monitor what is happening more easily.
{{% /notice %}}
