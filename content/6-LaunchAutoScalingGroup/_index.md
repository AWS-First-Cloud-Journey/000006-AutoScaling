---
title : "Initialize Auto Scaling Group"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

#### Initialize Auto Scaling Group

In this section, we will implement an Auto Scaling Group for FCJ Management application to ensure our application will be deployed with high availability, and potentially increase the number of EC2 instances when users visit. into the boost system.

1. Access to **EC2**

- Select **Auto Scaling Groups**
- Select **Create Auto Scaling group**


![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0001-createasg.png?featherlight=false&width=90pc)

2. **Auto Scaling Group name**, enter **```FCJ-Management-ASG```**


![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0002-createasg.png?featherlight=false&width=90pc)

3. Configure the template

- **Launch template**. select **FCJ-Management-template**
- Select **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0003-createasg.png?featherlight=false&width=90pc)

4. Configure **Network**

- **VPC**, select **asg-vpc**
- Select **AZ and subnet**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0004-createasg.png?featherlight=false&width=90pc)

5. Select **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0005-createasg.png?featherlight=false&width=90pc)

6. Configure **Load balancing**

- Select **Attach to an existing load balancer**
- Select **Choose from your load balancer target groups**
- Select **FCJ-Management-TG**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0006-createasg.png?featherlight=false&width=90pc)

7. Select **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0007-createasg.png?featherlight=false&width=90pc)

8. Configure group size and scaling policy.

- Desired capacity: Enter 1. (Default)
- Minimum capacity: Enter 1. (Default)
- Maximum capacity: Enter 3.

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0008-createasg.png?featherlight=false&width=90pc)

9. In the section **Scaling policies** - optional: Select this exercise to make it easier for the next step to be checked. You can completely set the resource scaling policy according to your needs.

- Select **Taget tracking scaling policy**
- **Scaling policy name**, enter **```Target Tracking Policy```**
- **Metric type**, select **Application Load Balancer request count per target**.
- **Target group**, enter **```FCJ-Management```**
- **Target value**, enter 30

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/0009-createasg.png?featherlight=false&width=90pc)

10. Select **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00010-createasg.png?featherlight=false&width=90pc)

11. Select **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00011-createasg.png?featherlight=false&width=90pc)

12. Select **Next**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00012-createasg.png?featherlight=false&width=90pc)

13. Select **Create Auto Scaling group**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00013-createasg.png?featherlight=false&width=90pc)

14. Completing the creation of **Auto Scaling groups**

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00014-createasg.png?featherlight=false&width=90pc)

15. The initialization process of the Auto Scaling Group will be done, the newly created Auto Scaling Group will be displayed in the list, and you can select it to view detailed information.

- We can track existing EC2 instances in Auto Scaling Group on the **Instance management** page. Instances with InService status are ready-to-go instances.

![Auto Scaling Group](/images/6-LaunchAutoScalingGroup/00015-createasg.png?featherlight=false&width=90pc)