---
title : "Check the result"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

#### Check the result

In this exercise, we will test access to ShareNote and proceed to increase the number of access requests to the application by opening multiple connections simultaneously using Webserver Stress Tool 8. Click here [Webserver Stress Tool 8](https://www.paessler.com/tools/webstress) to download.

1. Download **Webserver Stress Tool 8**

![Auto Scaling Group](/images/17/0001.png?featherlight=false&width=90pc)

2. Test the self-scalability of the deployed FCJ Management application

   - Extract the zip file and install Webserver Stress Tool 8 with default options.
   - Start Webserver Stress Tool 8 to proceed to create a large amount of access to the Endpoint of the Load Balancer.
   - Click on the Test Type tab and enter the parameters as shown below:
   - Run Unit : 100000
   - Number of Users : 101
   - Click Delay : 1

![Auto Scaling Group](/images/17/0001.png?featherlight=false&width=90pc)

3. Click the URLs tab, copy the DNS name of the FCJ Management application into the URL box (the DNSName when you created the Load Balancer in step 5. Initialize the Load Balancer), and click **Start Test**

![Auto Scaling Group](/images/17/0002.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/0003.png?featherlight=false&width=90pc)

4. After some time, check the response of the Auto Scaling Group. We see the number of instances is increased to the maximum number that we set to 3.


![Auto Scaling Group](/images/17/0004.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/0006.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/0008.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/0009.png?featherlight=false&width=90pc)

5. Check that access to the application from the browser is not interrupted.


![Load Balancer](/images/15/0009.png?featherlight=false&width=90pc)

6. View logfile results

![Auto Scaling Group](/images/17/0005.png?featherlight=false&width=90pc)

![Auto Scaling Group](/images/17/0007.png?featherlight=false&width=90pc)

7. See how **EC2** looks when running the application.

![Auto Scaling Group](/images/17/00010.png?featherlight=false&width=90pc)

Congratulations on completing the FCJ Management practice session with Auto Scaling Group and Elastic Load Balancer.

You will receive an email notification.

![Auto Scaling Group](/images/17/00013.png?featherlight=false&width=90pc)