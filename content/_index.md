---
title: "Deploying FCJ Management with Auto Scaling Group"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

# Deploying FCJ Management Application with Auto Scaling Group

#### Overview

**ℹ️ Information**: In this workshop, you will deploy an application with Amazon EC2 Auto Scaling to ensure dynamic scalability based on fluctuating workloads. Additionally, you will implement Elastic Load Balancing to distribute traffic and efficiently manage user requests to your application tier.

Make sure to review the [Deploying FCJ Management Application on a Windows/Amazon Linux Virtual Machine](https://000004.awsstudygroup.com/) documentation to understand the base deployment process. We will leverage this foundation to implement a highly available, fault-tolerant architecture using AWS's elastic scaling capabilities.

**💡 Pro Tip**: Auto Scaling Groups combined with Application Load Balancers create a resilient architecture that can automatically adjust capacity to maintain performance during traffic spikes while optimizing costs during periods of low demand.

**🔒 Security Note**: This architecture follows AWS Well-Architected Framework principles, ensuring your application deployment meets industry best practices for reliability, performance efficiency, and cost optimization.

#### Contents

1. [Introduction](1-introduction/)
2. [Preparation](2-preparation/)
3. [Create Launch Template](3-create-launch-template/)
4. [Setup Load Balancer](4-setup-load-balancer/)
5. [Test](5-test/)
6. [Create Auto Scaling Group](6-create-auto-scaling-group/)
7. [Test Solutions](7-test-solutions/)
8. [Clean up Resources](8-cleanup/)
