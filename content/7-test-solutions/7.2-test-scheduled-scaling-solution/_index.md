---
title: "Test scheduled scaling solution"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>7.2. </strong>"
---

#### Overview

**ℹ️ Information**: Scheduled Scaling enables you to configure your Auto Scaling Group to automatically adjust capacity based on predictable load changes. This approach is ideal for workloads with consistent patterns that occur at specific times daily, weekly, or seasonally.

#### Test Environment Setup

Since we've already configured our load testing environment in the previous section, we'll continue using those settings for consistency in our comparison of scaling methods.

#### Configuring Scheduled Scaling

To implement scheduled scaling:

1. Navigate to your Auto Scaling Group details page
2. Select the **Automatic scaling** tab
3. Scroll to the **Scheduled actions** section at the bottom of the page

![Scheduled Actions Section](/images/7-test-solution/7.2.1.png?featherlight=false&width=90pc)

4. Click **Create scheduled action**

![Create Scheduled Action Button](/images/7-test-solution/7.2.2.png?featherlight=false&width=90pc)

5. Configure the scheduled action with these parameters:
   - Name: `Rush hour`
   - Desired capacity: **1**
   - Min: **1** (can be set to 0 depending on your requirements)
   - Max: **3**
   - Recurrence: **Once** (or select another pattern as needed)
   - Time zone: **Asia/Ho_Chi_Minh** (select your appropriate time zone)
   - Specific start time: Set to the nearest time from your current configuration
   - Click **Create** to implement the scheduled action

![Scheduled Action Configuration](/images/7-test-solution/7.2.3.png?featherlight=false&width=90pc)

**⚠️ Warning**: The Desired capacity, Min, and Max parameters will override the corresponding ASG settings during the scheduled period. When implementing multiple scaling types in production, carefully consider how these values interact with other scaling policies.

After successful creation, you'll see your scheduled action in the list:

![Scheduled Action Created](/images/7-test-solution/7.2.4.png?featherlight=false&width=90pc)

#### Testing the Scheduled Scaling

For effective testing:

1. Start your load testing program approximately 5 minutes before the scheduled scaling action is set to trigger

![Load Testing Program](/images/7-test-solution/7.2.5.png?featherlight=false&width=90pc)

2. When the scheduled time arrives, monitor the **Activity** tab of your ASG
3. You should observe the **Executing scheduled action Rush hour** event triggering at the configured time, followed by the launch of a new instance

![ASG Activity Log](/images/7-test-solution/7.2.6.png?featherlight=false&width=90pc)

#### Analyzing the Results

To evaluate the effectiveness of scheduled scaling:

1. Return to the EC2 Console and examine the instance metrics (note that metrics update every 15 minutes)
2. Focus on the CPU Utilization chart to observe the impact of your test

![Initial CPU Metrics](/images/7-test-solution/7.2.7.png?featherlight=false&width=90pc)

**💡 Pro Tip**: In this example, you can see a CPU utilization spike between 14:30 and 14:40, which corresponds to when we initiated the load test. After the new instance was added by the scheduled action, the load was distributed, resulting in the subsequent decline.

3. For more detailed analysis, select the newly launched instance and adjust the chart view:
   - Select **1h** timeframe
   - Select **1 second** granularity

![Detailed CPU Metrics](/images/7-test-solution/7.2.9.png?featherlight=false&width=90pc)

This granular view clearly shows how the scheduled scaling action affected system performance.

#### Real-World Applications

**ℹ️ Information**: Scheduled Scaling is particularly valuable for applications with predictable usage patterns:

- Financial trading platforms with market opening/closing traffic spikes
- E-commerce sites during daily peak shopping hours
- Enterprise applications with business-hour usage patterns
- Batch processing jobs that run at specific times

**🔒 Security Note**: While scheduled scaling helps optimize resource utilization, it's important to maintain minimum capacity levels that can handle unexpected traffic surges or potential DDoS attacks outside of scheduled scaling periods.

#### Conclusion

Scheduled Scaling provides a proactive approach to capacity management for workloads with predictable patterns. However, for maximum resilience and cost efficiency, AWS recommends combining scheduled scaling with other scaling types:

- Use scheduled scaling for predictable, time-based patterns
- Implement dynamic scaling to handle unexpected traffic variations
- Consider predictive scaling for workloads with complex but recurring patterns

This multi-layered approach ensures your application remains responsive while optimizing resource utilization and cost.
