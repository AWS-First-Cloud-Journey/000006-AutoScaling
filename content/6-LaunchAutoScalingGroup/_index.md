---
title : "Create Auto Scaling Group"
date : "`r Sys.Date()`"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---


#### Create Auto Scaling Group

In this section, we will implement an Auto Scaling Group for the FCJ Management application to ensure our application will be deployed with high availability and potentially increase the number of EC2 instances when users visit, into the boost system.

1. Access to **EC2**

   - Select **Auto Scaling Groups**
   - Select **Create Auto Scaling group**

![Auto Scaling Group](/images/16/0001.png?featherlight=false&width=90pc)

2. **Auto Scaling Group name**, enter `FCJ-Management-ASG`

![Auto Scaling Group](/images/16/0002.png?featherlight=false&width=90pc)

3. Configure the template

   - **Launch template**, select `FCJ-Management-template`
   - Select **Next**

![Auto Scaling Group](/images/16/0003.png?featherlight=false&width=90pc)

4. Configure **Network**

   - **VPC**, select created.
   - Select **AZ and subnet**

![Auto Scaling Group](/images/16/0004.png?featherlight=false&width=90pc)

5. Select **Next**

![Auto Scaling Group](/images/16/0005.png?featherlight=false&width=90pc)

6. Configure **Load balancing**

   - Select **Attach to an existing load balancer**
   - Select **Choose from your load balancer target groups**
   - Select `FCJ-Management-TG`

![Auto Scaling Group](/images/16/0006.png?featherlight=false&width=90pc)

7. Select **Next**

![Auto Scaling Group](/images/16/0007.png?featherlight=false&width=90pc)

8. Configure group size and scaling policy.

   - Desired capacity: Enter 1. (Default)
   - Minimum capacity: Enter 1. (Default)
   - Maximum capacity: Enter 3.

![Auto Scaling Group](/images/16/0008.png?featherlight=false&width=90pc)

9. Under **Scaling policies** - optional: Select this exercise to make it easier for the next step to be checked. You can completely set the resource scaling policy according to your needs.

   - Select **Target tracking scaling policy**
   - **Scaling policy name**, enter `Target Tracking Policy`
   - **Metric type**, select **Application Load Balancer request count per target**.
   - **Target group**, enter `FCJ-Management`
   - **Target value**, enter 30

![Auto Scaling Group](/images/16/0009.png?featherlight=false&width=90pc)

10. Select **Next**

![Auto Scaling Group](/images/16/00010.png?featherlight=false&width=90pc)

11. Select **Create a topic**.

![Auto Scaling Group](/images/16/00011.png?featherlight=false&width=90pc)

12. Configure **Add notifications**. Select **Next**

![Auto Scaling Group](/images/16/00012.png?featherlight=false&width=90pc)

- Check email and **Confirm subscription**

![Auto Scaling Group](/images/17/00011.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/00012.png?featherlight=false&width=90pc)

13. Select **Create Auto Scaling group**

![Auto Scaling Group](/images/16/00013.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00014.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00015.png?featherlight=false&width=90pc)

14. Complete creation **Auto Scaling groups**

![Auto Scaling Group](/images/16/00016.png?featherlight=false&width=90pc)

15. The initialization of the Auto Scaling Group will be done, the newly created Auto Scaling Group will be displayed in the list, and you can select it to view detailed information.

    - We can track existing EC2 instances in the Auto Scaling Group on the **Instance management** page. Instances with InService status are ready-to-go instances.

![Auto Scaling Group](/images/16/00017.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00018.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/16/00019.png?featherlight=false&width=90pc)
