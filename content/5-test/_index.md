---
title: "Test"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: "<strong>5. </strong>"
---

#### Overview

**ℹ️ Information**: In this section, we'll verify that our application is properly deployed behind the Application Load Balancer and functioning as expected. This testing phase ensures our infrastructure is correctly configured before proceeding to auto scaling implementation.

#### Accessing the Application

To test the deployment:

1. Navigate to the EC2 console and select **Load Balancers**
2. Locate the **FCJ-Management-LB** and copy its DNS name
3. Paste the DNS name into your browser's address bar

![Accessing the Application via Load Balancer DNS](/images/5-test/5.1.png?featherlight=false&width=90pc)

**💡 Pro Tip**: The DNS name of your Application Load Balancer follows the format `name-1234567890.region.elb.amazonaws.com` and is globally resolvable, allowing access from anywhere with internet connectivity.

#### Verifying Application Functionality

Upon successful connection, you should see the FCJ Management application interface:

![Application Interface](/images/5-test/5.2.png?featherlight=false&width=90pc)

#### Testing CRUD Operations

To verify complete functionality, test the application's data manipulation capabilities:

1. Select a record and click the edit button to modify its information

![Editing a Record](/images/5-test/5.3.png?featherlight=false&width=90pc)

2. After entering the updated information, click **Submit**
3. Verify you receive a success notification

![Update Confirmation](/images/5-test/5.4.png?featherlight=false&width=90pc)

4. Return to the homepage to confirm the changes are reflected in the database

![Updated Record Verification](/images/5-test/5.5.png?featherlight=false&width=90pc)

**⚠️ Warning**: If you encounter any errors during testing, verify that your security groups are properly configured to allow traffic on port 5000 and that your target group health checks are passing.

#### Performance Monitoring

**ℹ️ Information**: In subsequent testing steps, we'll focus on monitoring application metrics through Amazon CloudWatch. While reviewing these metrics, pay attention to any performance degradation that might occur during periods of increased load.

**🔒 Security Note**: All traffic to your application is now flowing through the Application Load Balancer, which provides an additional security layer by isolating your EC2 instances from direct internet access. Consider implementing AWS WAF with your ALB for additional protection against common web exploits.
