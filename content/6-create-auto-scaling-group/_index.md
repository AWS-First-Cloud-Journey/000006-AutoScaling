---
title: "Create Auto Scaling Group"
date: "`r Sys.Date()`"
weight: 6
chapter: false
pre: "<strong>6. </strong>"
---

#### Overview

**ℹ️ Information**: Auto Scaling Groups automatically adjust your application's compute capacity based on demand, ensuring optimal performance while controlling costs. In this section, we'll configure an Auto Scaling Group to dynamically manage our EC2 instances behind the Application Load Balancer.

#### Understanding the Need for Auto Scaling

**⚠️ Warning**: Our testing revealed performance instability when the application receives high traffic volumes. While manually adding EC2 instances and distributing traffic with a Load Balancer helps, this approach is impractical for several reasons:

- Each new instance requires manual configuration with the application and dependencies
- Responding to traffic fluctuations requires constant monitoring
- Manual scaling cannot efficiently respond to unexpected traffic spikes

Auto Scaling solves these challenges by automatically adjusting capacity based on defined policies.

#### Creating an Auto Scaling Group

Navigate to the Auto Scaling Group creation interface:

1. In the EC2 management console:
   - Scroll down the left navigation panel
   - Select **Auto Scaling Groups**
   - Click **Create Auto Scaling group**

![Auto Scaling Group Creation Interface](/images/6-create-auto-scaling-group/6.1.png?featherlight=false&width=90pc)

#### Configuring Launch Template

In the Auto Scaling group creation wizard:

1. Basic configuration:
   - Name: `FCJ-Management-ASG`
   - Launch template: select `FCJ-Management-template`
   - Version: **Default (1)**

![Launch Template Selection](/images/6-create-auto-scaling-group/6.2.png?featherlight=false&width=90pc)

**ℹ️ Information**: The launch template contains all the configuration details needed to launch instances, including the AMI, instance type, key pair, security groups, and user data scripts.

![Launch Template Configuration](/images/6-create-auto-scaling-group/6.3.png?featherlight=false&width=90pc)

**⚠️ Warning**: The ASG name should match the name specified in section **2.6** for Predictive Scaling configuration. The launch template must include all required components (MySQL Client, Node.js, application source code, and PM2) for proper instance functionality.

#### Configuring Network Settings

In the network configuration section:

1. VPC: select **AutoScaling-Lab**
2. Availability Zones and subnets: select all **3 public subnets**
3. Click **Next**

![Network Configuration](/images/6-create-auto-scaling-group/6.4.png?featherlight=false&width=90pc)

**💡 Pro Tip**: Distributing instances across multiple Availability Zones improves application reliability. If one AZ experiences issues, instances in other AZs continue serving traffic.

#### Configuring Load Balancer Integration

Connect your Auto Scaling Group to the previously created load balancer:

1. Load balancing: select **Attach to an existing load balancer**
2. Attachment method: choose **Choose from your load balancer target groups**
3. Target group: select **FCJ-Management-TG | HTTP**

![Load Balancer Integration](/images/6-create-auto-scaling-group/6.5.png?featherlight=false&width=90pc)

**ℹ️ Information**: When properly configured, the dropdown will display your existing target group, confirming that both the Application Load Balancer and Target Group are correctly set up.

For additional configuration:

1. VPC Lattice integration: select **No VPC Lattice service**
2. Health checks: enable **Turn on Elastic Load Balancing health checks**
3. Leave remaining health check settings as default

![Health Check Configuration](/images/6-create-auto-scaling-group/6.6.png?featherlight=false&width=90pc)

Under Monitoring:

1. Select **Enable group metrics collection within CloudWatch**
2. Click **Next**

![Monitoring Configuration](/images/6-create-auto-scaling-group/6.7.png?featherlight=false&width=90pc)

**💡 Pro Tip**: CloudWatch metrics provide valuable insights into your Auto Scaling Group's performance, helping you fine-tune scaling policies and troubleshoot issues.

#### Configuring Group Size and Scaling Policies

Define the initial capacity and scaling boundaries:

1. Group size:
   - Desired capacity: **1**
2. Scaling limits:
   - Minimum capacity: **1**
   - Maximum capacity: **3**

![Group Size Configuration](/images/6-create-auto-scaling-group/6.8.png?featherlight=false&width=90pc)

For scaling policies:

1. Select **No scaling policies** (we'll configure these in later sections)

![Scaling Policies Configuration](/images/6-create-auto-scaling-group/6.9.png?featherlight=false&width=90pc)

For instance maintenance:

1. Select **No policy**

![Instance Maintenance Configuration](/images/6-create-auto-scaling-group/6.10.png?featherlight=false&width=90pc)

**ℹ️ Information**: We're deferring scaling policy configuration because we'll implement and compare multiple scaling strategies in subsequent sections.

#### Configuring Notifications

Set up Amazon SNS notifications to monitor Auto Scaling events:

1. Notification configuration:
   - SNS topic: `asg-topic`
   - Recipients: enter your email address
   - Event types: select all event types
2. Click **Next**

![Notification Configuration](/images/6-create-auto-scaling-group/6.11.png?featherlight=false&width=90pc)

![Event Type Selection](/images/6-create-auto-scaling-group/6.12.png?featherlight=false&width=90pc)

Review your configuration and click **Create Auto Scaling group**.

![Review Configuration](/images/6-create-auto-scaling-group/6.13.png?featherlight=false&width=90pc)

**🔒 Security Note**: Notifications provide real-time awareness of scaling events, helping you monitor for unexpected behavior that could indicate security issues or application problems.

#### Verifying Auto Scaling Group Creation

After creation, you'll receive confirmation emails:

1. First, a subscription confirmation email (requires confirmation)

![Subscription Confirmation](/images/6-create-auto-scaling-group/6.14.png?featherlight=false&width=90pc)

2. Then, a notification when the first instance launches

![Instance Launch Notification](/images/6-create-auto-scaling-group/6.15.png?featherlight=false&width=90pc)

![Email Notification](/images/6-create-auto-scaling-group/6.16.png?featherlight=false&width=90pc)

Verify the Auto Scaling activity in the AWS Management Console:

1. Select your Auto Scaling Group
2. Navigate to the **Activity** tab to view scaling events

![Activity Verification](/images/6-create-auto-scaling-group/6.17.png?featherlight=false&width=90pc)

**⚠️ Warning**: As we implement different scaling strategies in subsequent sections, you may receive numerous notification emails. This is intentional to help you monitor scaling activities.

**💡 Pro Tip**: Auto Scaling Groups work best when combined with CloudWatch alarms that trigger scaling actions based on metrics like CPU utilization, network traffic, or custom application metrics. We'll explore these options in upcoming sections.
