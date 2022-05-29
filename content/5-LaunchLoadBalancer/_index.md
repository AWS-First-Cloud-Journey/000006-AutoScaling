---
title : "Initialize Load Balancer"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Initialize Load Balancer

1. Access to **EC2**

- Select **Load Balancers**
- Select **Create Load Balancer**


![Load Balancer](/images/5-LaunchLoadBalancer/0001-createloadbalancer.png?featherlight=false&width=90pc)

2. Section **Load balancer types**

- Select **HTTP/HTTPS**
- Select **Create**

![Load Balancer](/images/5-LaunchLoadBalancer/0002-createloadbalancer.png?featherlight=false&width=90pc)

3. In the **Create Application Load Balancer** interface

- **Load balancer name**, enter **```FCJ-Management-LB```**
- **Scheme**, select **Internet-facing**
- **IP address type**, select **IPv4**

![Load Balancer](/images/5-LaunchLoadBalancer/0003-createloadbalancer.png?featherlight=false&width=90pc)

4. Configure **Network mapping**

- **VPC**, select **asg-vpc**
- **Mapping**, select **ap-southeast-1a** and **ap-southeast-1b**
- Select **subnet**

![Load Balancer](/images/5-LaunchLoadBalancer/0004-createloadbalancer.png?featherlight=false&width=90pc)

5. Configure **security group**, select **FCJ-Management-SG**.

- Section **Listeners and routing**, in **Default actions** select **FCJ-Management-TG**

![Load Balancer](/images/5-LaunchLoadBalancer/0005-createloadbalancer.png?featherlight=false&width=90pc)

6. Check again and select **Create load balancer**

![Load Balancer](/images/5-LaunchLoadBalancer/0006-createloadbalancer.png?featherlight=false&width=90pc)

7. Create **Application Load Balancer** successfully and select **View load balancer**

![Load Balancer](/images/5-LaunchLoadBalancer/0007-createloadbalancer.png?featherlight=false&width=90pc)

8. In the **Load Balancer** interface. The Load Balancer creation process will take about 5-10 minutes to complete. You can check the status change from provisioning to active in the Load Balancer list.

- Select **FCJ-Management-LB**
- Copy **DNS name** of Load Balancer.

![Load Balancer](/images/5-LaunchLoadBalancer/0008-createloadbalancer.png?featherlight=false&width=90pc)

9. Access by pasting **DNS name** into the browser. However, at the moment we only have a single EC2 server.


![Load Balancer](/images/5-LaunchLoadBalancer/0009-createloadbalancer.png?featherlight=false&width=90pc)

Next, we will proceed to configure the Auto Scaling Group feature, which automatically increases the number of our EC2 instances when the traffic is high.