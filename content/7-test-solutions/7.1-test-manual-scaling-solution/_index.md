---
title: "Test manual scaling solution"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>7.1. </strong>"
---

### Manual Scaling

Manual Scaling is performed by manually adjusting the **Desired capacity** of the ASG. After adjusting and confirming the update, wait for a while, and the ASG will update the number of instances and proceed to either launch or terminate EC2 Instances depending on the **Desired capacity** setting.

#### Test Setup

Once the Auto Scaling Group is created, the service will automatically launch an EC2 Instance according to the configuration. To verify this, you can check the EC2 Console:

- Select **Load Balancer**
- Choose the **Resource map - new** tab

Here, you will see the Target Group linked to two Targets, which are two EC2 Instances (one is the original instance created, and the other is the instance created by ASG).

![7.1.1](/images/7-test-solution/7.1.1.png)

Now, test the application that we downloaded earlier.

- Open the application and click on the **Test Type** tab
- Test Type:
  - Select **CLICKS**
  - Run until: **100000**
- User Simulation
  - Number Of Users: **1000**
  - Click Delay: **1** second

![7.1.2](/images/7-test-solution/7.1.2.png)

In the URLs tab, configure the following information:

- Name: `Manual Scaling Test` (you can name it anything since we will use it to test other scaling methods later).
- URL: Copy the DNS of the Load Balancer and paste it.

![7.1.3](/images/7-test-solution/7.1.3.png)

On the toolbar, click **Start Test**.

![7.1.4](/images/7-test-solution/7.1.4.png)

#### Running the Test

Now go back to the AWS Management Console, in the EC2 Console:

- Select both EC2 Instances in the target group
- Click on the **Monitoring** tab and start observing

In this section, there are 7 charts, but for now, we only care about the following 5 charts:

- CPU Utilization (%): This chart shows the CPU resource usage of the two instances, each below 8%.
- Network in (bytes): This chart shows the incoming network traffic to the two instances, each under 2.9 million Megabytes.
- Network out (bytes): This chart shows the outgoing network traffic from the two instances, each under 17.3 million Megabytes.
- Network packets in (count): This chart shows the number of packets coming into the two instances, each under 6.85 thousand packets.
- Network packets out (count): This chart shows the number of packets going out from the two instances, each under 7.36 thousand packets.

![7.1.5](/images/7-test-solution/7.1.5.png)

{{% notice note %}}
From now on, we will read the charts this way, including important metrics in the vertical, horizontal axes, and plotted lines. This will help us better understand how the Load Balancer distributes network traffic to instances in the Target Group.
{{% /notice %}}

{{% notice note %}}
If you select only one instance, the chart will show just one line representing that instance. The more instances you select from the list, the more lines will be shown on the graph.
{{% /notice %}}

#### Manually Adjusting the Desired Capacity of ASG

Now, let’s return to the details page of the ASG we created earlier. In the Group details section, we can see: **Desired capacity = 1**.

Let's assume it's off-peak hours, and we want to turn off one instance to save costs. To do this, we manually adjust the **Desired capacity = 0**. Click **Edit**.

![7.1.6](/images/7-test-solution/7.1.6.png)

A Group size dialog will appear. Adjust the Desired capacity and Min desired capacity to **0** and click **Update**.

![7.1.7](/images/7-test-solution/7.1.7.png)

Then, go to the Activity tab to check what the ASG is doing.

![7.1.8](/images/7-test-solution/7.1.8.png)

{{% notice note %}}
While the instance is being shut down, you can stop the test program.
{{% /notice %}}

=> We can see that the ASG automatically terminates an instance based on the configured settings.

A few minutes later, if you return to the Load Balancer details page and go to the **Resource map - new** tab, you'll see that there is now only one target remaining.

![7.1.9](/images/7-test-solution/7.1.9.png)

{{% notice note %}}
At this point, REMEMBER TO RESTART the test program.
{{% /notice %}}

We will also receive an email from SNS.

![7.1.10](/images/7-test-solution/7.1.10.png)

When there is high traffic, the application's performance may slow down slightly. You can open the application via the Load Balancer's DNS to test.

![7.1.11](/images/7-test-solution/7.1.11.png)

Now, go back to the EC2 Console, select the remaining target, and observe the charts.

![7.1.12](/images/7-test-solution/7.1.12.png)

We can see that the instance is now handling almost double the network traffic, and its CPU resource usage has nearly quadrupled.

#### Conclusion

In reality, systems will involve more complex and time-consuming processes, consuming more CPU resources. In this tutorial, we only tested GET requests, but in real cases, the requests will be much more complicated.
