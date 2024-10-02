---
title: "Test solutions"
date: "`r Sys.Date()`"
weight: 7
chapter: false
pre: "<strong>7. </strong>"
---

### Scaling Solutions / Techniques

The **Auto Scaling Group** service provides different scaling solutions depending on the needs and usage levels of our system. Therefore, we need to calculate, estimate, observe, and plan the use of each type or combine them to increase the flexibility of the system.

In this section, we will go through each solution, but before diving into the details, let's take a brief look at these scaling solutions.

#### Manual scaling

We manually scale up or down the targets in a Target Group by adjusting the Desired capacity parameter in the **Auto Scaling Group**. This action is called Manual Scaling. In certain quick, individual situations, we may need to add or remove targets manually.

#### Scheduled scaling

When we understand the network traffic in and out of the system or the time when targets operate at near-maximum capacity, and this activity is consistent and long-term (possibly annually), we can schedule (and set a timer) for the **Auto Scaling Group** to scale up or down the targets.

#### Dynamic scaling

If the incoming network traffic to the system doesn't follow a predictable pattern and is hard to forecast, we can use the automatic scaling solution from ASG. In this case, ASG will use the Dynamic scaling policy configuration to scale the targets more appropriately for the system.

#### Predictive scaling

Another technique is that ASG can predict the network traffic for the next 3 or more days. For unpredictable systems, we can rely on this solution along with Dynamic scaling to increase system flexibility. This solution will show parameters based on how we configure it, but the general idea is to predict traffic and usage levels within the system.

{{% notice note %}}
Since we don't have data from the previous section, this is why we need to prepare and run sample data from **2.6 - Prepare metrics for predictive scaling** beforehand.
{{% /notice %}}

### Installing the test program

Before diving into this section, we need to download a test program to simulate a system under high traffic. First, go to this link to download the test program: [https://www.paessler.com/tools/webstress](https://www.paessler.com/tools/webstress)

![7.1](/images/7-test-solution/7.1.png)

We will download a RAR file, extract the installation file from it, and install the program. After installation, we will open the program and see the interface as shown below:

![7.2](/images/7-test-solution/7.2.png)

### Content

1. [Test the manual scaling solution](/7-test-solutions/7.1-test-manual-scaling-solution)
2. [Test the scheduled scaling solution](/7-test-solutions/7.2-test-scheduled-scaling-solution)
3. [Test the dynamic scaling solution](/7-test-solutions/7.3-test-dynamic-scaling-solution)
4. [Test the predictive scaling solution](/7-test-solutions/7.4-test-predictive-scaling-solution)

{{% notice info %}}
This section takes a lot of time and requires careful observation (you can test while running the simulations), so be patient and meticulous in observing the results.
{{% /notice %}}
