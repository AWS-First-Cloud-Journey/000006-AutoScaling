---
title: "Preparation"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<strong>2. </strong>"
---

In this exercise, we need to prepare some services to be able to deploy the FCJ Management application using Auto Scaling Group with Elastic Load Balancer. In general, we will deploy the ShareNote application according to the following architecture:
![Create VPC](/images/2-preparation/diagram0006.png)

### Content

1. [Setup network infrastructure](2.1-setup-network/)
2. [Launch EC2 instance](2.2-launch-ec2-instance/)
3. [Launch Database instance with RDS](2.3-launch-db-instance/)
4. [Setup data for database](2.4-add-data-to-db/)
5. [Deploy web server](2.5-deploy-web-server/)
6. [Prepare metric cho Predictive scaling](2.6-prepare-metrics-for-predictive-scaling/)
