---
title: "Test manual scaling solution"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>7.1. </strong>"
---

#### Overview

**ℹ️ Information**: Manual Scaling is performed by explicitly adjusting the **Desired capacity** parameter of your Auto Scaling Group. After modifying this value and confirming the update, the ASG will automatically launch or terminate EC2 instances to match your specified capacity.

#### Test Environment Setup

Once your Auto Scaling Group is created, the service automatically launches an EC2 instance according to your configuration. To verify this deployment:

1. Navigate to the EC2 Console
2. Select **Load Balancer**
3. Choose the **Resource map - new** tab

![Auto Scaling Group Initial State](/images/7-test-solution/7.1.1.png?featherlight=false&width=90pc)

**ℹ️ Information**: You should observe the Target Group linked to two targets - your original EC2 instance and the new instance created by the Auto Scaling Group.

#### Configuring the Load Test

Now we'll configure the load testing application downloaded earlier:

1. Open the application and navigate to the **Test Type** tab
2. Configure the following settings:
   - Test Type: **CLICKS**
   - Run until: **100000**
   - Number Of Users: **1000**
   - Click Delay: **1** second

![Load Test Configuration](/images/7-test-solution/7.1.2.png?featherlight=false&width=90pc)

3. In the URLs tab, enter:
   - Name: `Manual Scaling Test` (this can be customized as needed)
   - URL: Enter your Load Balancer's DNS name

![URL Configuration](/images/7-test-solution/7.1.3.png?featherlight=false&width=90pc)

4. Click **Start Test** on the toolbar to begin the load test

![Starting the Load Test](/images/7-test-solution/7.1.4.png?featherlight=false&width=90pc)

#### Monitoring Instance Performance

While the test is running, return to the AWS Management Console:

1. In the EC2 Console, select both EC2 instances in the target group
2. Click on the **Monitoring** tab to observe performance metrics

![Initial Performance Metrics](/images/7-test-solution/7.1.5.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Focus on these five key metrics to understand your application's performance under load:
- **CPU Utilization (%)**: Shows processor usage (currently below 8% for each instance)
- **Network in (bytes)**: Measures incoming traffic (under 2.9 million MB per instance)
- **Network out (bytes)**: Measures outgoing traffic (under 17.3 million MB per instance)
- **Network packets in (count)**: Shows incoming packet count (under 6.85 thousand packets per instance)
- **Network packets out (count)**: Shows outgoing packet count (under 7.36 thousand packets per instance)

**ℹ️ Information**: The charts display one line per selected instance. Selecting multiple instances allows you to compare their performance simultaneously, helping you understand how the Load Balancer distributes traffic.

#### Manually Scaling Down the ASG

To simulate cost optimization during off-peak hours:

1. Navigate to your Auto Scaling Group details page
2. Note the current setting: **Desired capacity = 1**
3. Click **Edit** to modify the capacity

![ASG Initial Configuration](/images/7-test-solution/7.1.6.png?featherlight=false&width=90pc)

4. In the Group size dialog, set both Desired capacity and Min desired capacity to **0**
5. Click **Update** to apply the changes

![Scaling Down Configuration](/images/7-test-solution/7.1.7.png?featherlight=false&width=90pc)

6. Navigate to the Activity tab to monitor the scaling action

![ASG Activity Log](/images/7-test-solution/7.1.8.png?featherlight=false&width=90pc)

**⚠️ Warning**: While the instance is being terminated, you should pause your load testing application to avoid potential errors.

**ℹ️ Information**: The ASG will automatically terminate an instance based on your updated configuration. After a few minutes, returning to the Load Balancer's Resource map will show only one remaining target.

![Scaled Down Resource Map](/images/7-test-solution/7.1.9.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Remember to restart your load testing program after the scaling operation completes to continue your testing.

#### Observing Notification and Performance Impact

After scaling down, you'll receive an email notification from Amazon SNS:

![SNS Notification](/images/7-test-solution/7.1.10.png?featherlight=false&width=90pc)

With reduced capacity, you may notice performance degradation when accessing your application through the Load Balancer's DNS:

![Application Performance](/images/7-test-solution/7.1.11.png?featherlight=false&width=90pc)

Return to the EC2 Console to observe the impact on your remaining instance:

![Single Instance Metrics](/images/7-test-solution/7.1.12.png?featherlight=false&width=90pc)

**ℹ️ Information**: The monitoring data clearly shows that the remaining instance is now handling approximately double the network traffic, with CPU utilization nearly quadrupled compared to the previous balanced state.

#### Conclusion

**⚠️ Warning**: This demonstration uses simple GET requests, but real-world applications typically involve more complex operations that consume significantly more CPU resources and may experience more dramatic performance impacts during scaling events.

**🔒 Security Note**: While manual scaling provides direct control over your infrastructure costs, it requires human intervention and monitoring, which can lead to delayed responses during unexpected traffic spikes. Consider implementing automated scaling policies for production workloads to maintain both performance and security.
