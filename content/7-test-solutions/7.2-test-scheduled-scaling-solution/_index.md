---
title: "Test scheduled scaling solution"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>7.2. </strong>"
---

### Scheduled Scaling

Scheduled Scaling allows us to inform the ASG when it should launch additional instances and when it should remove instances. This type of scaling is suitable for workloads that fluctuate over a certain period, recurring daily, and over a long period.

Since we've already set up the testing in the previous section, we don't need to set it up again, and we can continue using those settings.

#### Configuration

Go to the ASG information page, navigate to the "Automatic scaling" tab, and scroll to the bottom.

![7.2.1](/images/7-test-solution/7.2.1.png)

Under the "Scheduled actions" section, click **Create scheduled action**.

![7.2.2](/images/7-test-solution/7.2.2.png)

A form will appear. Fill in the details as follows:

- Name: `Rush hour`.
- Desired capacity: **1**.
- Min: **1** (you can set it to 0).
- Max: **3**.
- Recurrence: **Once** (or any other option).
- Time zone: **Asia/Ho_Chi_Minh**.
- Specific start time: Set it to the nearest time you're configuring.
- Click **Create** to create the scheduled action.

![7.2.3](/images/7-test-solution/7.2.3.png)

{{% notice note %}}
The parameters for Desired capacity, Min, and Max will all affect the corresponding ASG parameters, so in practice, you will need to combine multiple scaling types and carefully consider these settings.
{{% /notice %}}

Successfully created.

![7.2.4](/images/7-test-solution/7.2.4.png)

#### Testing

Approximately 5 minutes before the ASG launches instances as scheduled, we should run the test program.

![7.2.5](/images/7-test-solution/7.2.5.png)

After a few minutes, when the scheduled time for ASG to launch new instances arrives, go to the **Activity** tab to monitor ASG actions. You'll see the **Executing scheduled action Rush hour** event triggered at the right time, and then the ASG launches a new instance.

![7.2.6](/images/7-test-solution/7.2.6.png)

Returning to the EC2 Console, metrics are updated every 15 minutes. When you revisit to observe these metrics, focus on the CPU Utilization chart. You can see that between 14:30 and 14:40, there is a spike, which was caused when we started the test program.

![7.2.7](/images/7-test-solution/7.2.7.png)

Wait a few more minutes for these metrics to update. Once updated, select the newly launched instance.

![7.2.8](/images/7-test-solution/7.2.8.png)

You will notice that after 14:40, the chart declines.

Zoom in on this chart:

- Select **1h**.
- Select **1 second**.

![7.2.9](/images/7-test-solution/7.2.9.png)

You'll see the changes more clearly.

#### Conclusion

In reality, trading platforms often experience peak user traffic at certain times of the day. This increase in traffic is similar to rush hour in transportation, where traffic rises at a specific time each day and repeats daily for a long period. In such cases, we need to schedule new instances to handle the load.

However, in practice, we will need to combine this with other types of scaling to enhance the reliability of the system.
