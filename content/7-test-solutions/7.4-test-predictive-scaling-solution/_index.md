---
title: "Read metrics of predictive scaling solution"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: "<strong>7.4. </strong>"
---

### Predictive Scaling

From the traffic and workloads that the system receives and sends each day, ASG can "predict" the future traffic and workloads for the upcoming days. This helps ASG respond better by launching or terminating instances accordingly. Typically, Predictive Scaling is used in combination with other types of scaling.

#### Configuration

As in the previous section, I will manually scale in with ASG and wait for ASG to terminate all the instances created by this service.

![7.4.1](/images/7-test-solution/7.4.1.png)

Next, delete the automatic scaling policy to avoid affecting this test.

![7.4.2](/images/7-test-solution/7.4.2.png)

Then, go to the **Automatic Scaling** tab, scroll down to **Predictive scaling policies**, and click **Create predictive policy** to create a new one.

![7.4.3](/images/7-test-solution/7.4.3.png)

In this form, we will configure as follows:

- Policy details
  - Name: `PredictCPUUtilizationAt15Percent` (you can choose any name)
- Turn on scaling: enable **Scale based on forecast**. With the predictive scaling policy, essentially, it only makes predictions, but we can also use it to launch instances.

![7.4.4](/images/7-test-solution/7.4.4.png)

Next, in the **Metric and target utilization** section:

- Metrics: select **Custom metric pair**.
- Load metric: select **Custom CloudWatch metric**.
- Scaling metric: select **Custom CloudWatch metric**.

You will add custom metric JSON as follows:

- For **Load metric**

```json
{
  "CustomizedLoadMetricSpecification": {
    "MetricDataQueries": [
      {
        "Label": "Total CPU Utilization in ASG",
        "Id": "cpu_sum",
        "MetricStat": {
          "Metric": {
            "MetricName": "WSCustomCPUUTILIZATION",
            "Namespace": "FCJ Management Custom Metrics",
            "Dimensions": [
              {
                "Name": "AutoScalingGroupName",
                "Value": "FCJ-Management-ASG"
              }
            ]
          },
          "Stat": "Sum"
        },
        "ReturnData": true
      }
    ]
  }
}
```

- For **Scaling metric**

```json
{
  "CustomizedScalingMetricSpecification": {
    "MetricDataQueries": [
      {
        "Label": "Average CPU Utilization in ASG",
        "Id": "cpu_avg",
        "MetricStat": {
          "Metric": {
            "MetricName": "WSCustomCPUUTILIZATION",
            "Namespace": "FCJ Management Custom Metrics",
            "Dimensions": [
              {
                "Name": "AutoScalingGroupName",
                "Value": "FCJ-Management-ASG"
              }
            ]
          },
          "Stat": "Average"
        },
        "ReturnData": true
      }
    ]
  }
}
```

![7.4.5](/images/7-test-solution/7.4.5.png)

Next, check **Add custom capacity metric**.

Similarly to the previous two steps, I will add custom metric JSON for **Capacity metric**.

```json
{
  "CustomizedCapacityMetricSpecification": {
    "MetricDataQueries": [
      {
        "Label": "Number of instances in ASG",
        "Id": "capacity_avg",
        "MetricStat": {
          "Metric": {
            "MetricName": "WSCustomGroupInstances",
            "Namespace": "FCJ Management Custom Metrics",
            "Dimensions": [
              {
                "Name": "AutoScalingGroupName",
                "Value": "FCJ-Management-ASG"
              }
            ]
          },
          "Stat": "Average"
        },
        "ReturnData": true
      }
    ]
  }
}
```

![7.4.6](/images/7-test-solution/7.4.6.png)

{{% notice info %}}
If you configured **2.6 - Prepare metrics for predictive scaling** earlier, after completing the setup, you will see two charts displayed.
{{% /notice %}}

In the **Pre-launch instances** section of **Additional scaling settings - optional**, set it to **1 minute**. Click **Create** to create the policy.

![7.4.7](/images/7-test-solution/7.4.7.png)

{{% notice info %}}
Similar to Dynamic scaling, this Pre-launch instances setting will affect when the instances will be launched. For example, if ASG predicts a peak at 23:00, it will launch instances at 22:59, according to the configuration.
{{% /notice %}}

Check the results.

![7.4.8](/images/7-test-solution/7.4.8.png)

#### Reading Metrics from Sample Data

In that policy, you will see two charts: **Load** and **Capacity**. These charts provide data on previous traffic and the number of instances used in previous days, allowing predictions for the upcoming days, represented by the purple line.

![7.4.9](/images/7-test-solution/7.4.9.png)

{{% notice tip %}}
The chart is in UTC+0, and we are in UTC+7, so you'll need to add 7 hours when reading these charts.
{{% /notice %}}

First, focus on the chart on the left. At 15:00 UTC (which is 22:00 in Vietnam time), the total load was **164.546**.

![7.4.10](/images/7-test-solution/7.4.10.png)

To understand what this number represents, look at the chart on the right.

![7.4.11](/images/7-test-solution/7.4.11.png)

We can see that at that time, 13 instances were predicted to be launched, and the load correlates with these instances.

You can check other times as well.

![7.4.12](/images/7-test-solution/7.4.12.png)

![7.4.13](/images/7-test-solution/7.4.13.png)

If you wait for the predicted time, go to the ASG's Activity tab, and you'll see that ASG launches a new instance at 21:59, one minute before 22:00, as predicted above.

![7.4.14](/images/7-test-solution/7.4.14.png)

#### Conclusion

We can combine Predictive Scaling with Dynamic Scaling or other scaling types to increase ASG's flexibility and the system's reliability. For systems with consistent load over time, using predictive scaling is also a reasonable approach.
