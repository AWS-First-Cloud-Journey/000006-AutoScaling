---
title: "Cleanup Resources"
date: "`r Sys.Date()`"
weight: 8
chapter: false
pre: "<strong>8. </strong>"
---

### Cleanup Resources

After completing the workshop, we will proceed with the cleanup of resources.

#### Delete Auto Scaling Group

In the EC2 management interface, on the left navigation pane, scroll down and select **Auto Scaling Groups**.

- Select the Auto Scaling Group **FCJ-Management-ASG**
- Click the **Actions** button at the top right of the screen
- Choose **Delete**

![8.1](/images/8-Cleanup/8.1.png)

#### Delete Load Balancer

In the EC2 management interface, on the left navigation pane, scroll down and select **Load Balancer**.

- Select the Load Balancer **FCJ-Management-LB**
- Click the **Actions** button at the top right of the screen
- Choose **Delete load balancer**

![8.2](/images/8-Cleanup/8.2.png)

#### Delete Target Group

In the EC2 management interface, on the left navigation pane, scroll down and select **Target Group**.

- Select the Target Group **FCJ-Management-TG**
- Click the **Actions** button at the top right of the screen
- Choose **Delete**

![8.3](/images/8-Cleanup/8.3.png)

#### Delete Launch Template

In the EC2 management interface, on the left navigation pane, scroll down and select **Launch Templates**.

- Select the Launch Template **FCJ-Management-TG**
- Click the **Actions** button at the top right of the screen
- Choose **Delete template**

![8.4](/images/8-Cleanup/8.4.png)

#### Deregister AMI

In the EC2 management interface, on the left navigation pane, scroll down and select **AMIs**.

- Select the AMI **FCJ-Management-AMI**
- Click the **Actions** button at the top right of the screen
- Choose **Deregister AMI**

![8.5](/images/8-Cleanup/8.5.png)

#### Terminate EC2 Instance

In the EC2 management interface, on the left navigation pane, select **Instances**.

- Select the **FCJ-Management** instance
- Click the **Instance state** button at the top right of the screen
- Choose **Terminate (delete) instance**

![8.6](/images/8-Cleanup/8.6.png)

#### Delete RDS Database

- Access **RDS**
- On the left navigation pane, select **Databases**
- Select the database instance **fcj-management-db-instance** related to the lab.
- Click **Modify**.

![8.7](/images/8-Cleanup/8.7.png)

In the Modify DB Instance section, scroll down to the bottom:

- Uncheck **Enable deletion protection**
- Click **Continue**

![8.8](/images/8-Cleanup/8.8.png)

Continue in the Schedule modifications section:

- Select **Apply immediately**
- Click **Modify DB instance**

![8.9](/images/8-Cleanup/8.9.png)

Proceed to delete the DB instance:

- Select the database instance **fcj-management-db-instance**
- Click the **Actions** button at the top right of the screen
- Choose **Delete**

![8.10](/images/8-Cleanup/8.10.png)

- Select **I acknowledge that upon instance deletion, automated, including system snapshots and point-in-time recovery, will no longer be available**
- Enter **delete me**
- Click **Delete**

![8.11](/images/8-Cleanup/8.11.png)

#### Delete Subnet Group

- Select **Subnet groups**
- Select the subnet group **fcj-management-subnet-group**
- Click **Delete**

![8.12](/images/8-Cleanup/8.12.png)
