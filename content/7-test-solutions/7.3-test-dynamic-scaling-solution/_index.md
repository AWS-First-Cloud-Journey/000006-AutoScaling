---
title: "Test dynamic scaling solution"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<strong>7.3. </strong>"
---

### Dynamic Scaling

Dynamic scaling is based on the metrics provided by CloudWatch. Depending on how we configure it, ASG will either launch or terminate instances. We can configure ASG to launch a new instance when the CPU resources of an instance or instances exceed 90%, or if the network traffic is high, or if the number of packets sent to each instance is large.

Depending on the system and requirements, we will configure it differently. In this example, we will configure it based on the "number of packets sent to each instance."

#### Configuration

Before testing, we will manually scale in by terminating one instance. Then, go to the Activity tab and check again.

![7.3.1](/images/7-test-solution/7.3.1.png)

![7.3.2](/images/7-test-solution/7.3.2.png)

After deleting, we will now configure dynamic scaling. Go to the **Automatic scaling** tab.

- Click **Create dynamic scaling policy** to create a new scaling policy.

![7.3.3](/images/7-test-solution/7.3.3.png)

In this form, fill in the following details:

- Policy type: **Target tracking scaling**.
- Scaling policy name: `Request Over 500 per target`.
- Metric type: **Application Load Balancer request count per target**.
- Target group: **FCJ-Management-TG**.
- Target value: **500** (requests).
- Instance warmup: **60 seconds** (it is recommended to set a higher value).
- Click **Create** to create the policy.

![7.3.4](/images/7-test-solution/7.3.4.png)

{{% notice info %}}
The **Instance warmup** parameter affects the time an instance starts receiving external traffic. Specifically, when an instance is created and in the **InService** state (ready to operate), you can adjust the time it takes for an instance to begin receiving and processing requests. This time is called **instance warmup**. Adjusting this parameter allows more time for the instance to become fully stable, as the application may need to update and install dependencies or connect to other services to function properly.
{{% /notice %}}

Result:

![7.3.5](/images/7-test-solution/7.3.5.png)

#### Testing

Start the test program.

![7.3.6](/images/7-test-solution/7.3.6.png)

Go to the EC2 Console to see how many requests are being sent to EC2.

![7.3.7](/images/7-test-solution/7.3.7.png)

{{% notice note %}}
Wait a moment for the metrics to update. You'll notice that the graphs are trending upwards or stabilizing.
{{% /notice %}}

Return to the **Activity** tab of ASG. You will see 3 instances have been launched. Since the request volume is high, ASG calculates that it needs to create the maximum desired number of instances.

![7.3.8](/images/7-test-solution/7.3.8.png)

Go back to the EC2 Console, select all the newly created instances, and observe the charts.

![7.3.9](/images/7-test-solution/7.3.9.png)

You will notice that the green line is gradually going down, and other lines are starting to appear.

{{% notice note %}}
As mentioned before, metrics update every 15 minutes, so you will need to wait a bit to see the results.
{{% /notice %}}

Now, we will stop the test program.

![7.3.10](/images/7-test-solution/7.3.10.png)

Go to the ASG Activity tab and wait for ASG to terminate the unnecessary instances. This process may take a while.

![7.3.11](/images/7-test-solution/7.3.11.png)

#### Conclusion

When ASG detects that the system is becoming overloaded based on certain metrics, it will launch additional instances to bring the system back to a stable state. However, dynamic scaling is not very fast, as mentioned earlier. When scaling policies are created, they impact the core metrics, and ASG will "look" at them to decide whether to scale up or down.

As a result, the number of instances is calculated and updated at a slower pace. To address this, we can use Predictive Scaling, which allows ASG to react more quickly.
