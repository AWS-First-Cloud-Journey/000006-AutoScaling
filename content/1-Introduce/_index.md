---
title : "Introduction"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 1. </b> "
---

#### Introduce

In this exercise, we will be deploying the application using an Auto Scaling Group to ensure the application's scalability based on user demand. Additionally, we will implement a Load Balancer to distribute the load and manage user access requests to our Application Tier.

Before proceeding, please review the document [Deploying FCJ Management Application on a Windows/AmazonLinux Virtual Machine] to understand how to deploy the application on a virtual machine. We will utilize the virtual machine where **FCJ Management** is deployed for the purpose of mass deployment and scaling within the Auto Scaling Group.

#### Auto Scaling Group

An **Auto Scaling Group** is a collection of EC2 Instances that can dynamically adjust the number of its members according to the defined scaling policy.

#### Launch Template

A **Launch Template** is a feature that allows you to create a template for initializing EC2 Instances. This simplifies and streamlines the process of creating EC2 Instances for use within the Auto Scaling service.

#### Load Balancer

A **Load Balancer** is a tool used to evenly distribute incoming data traffic to AWS resources, specifically EC2 Instances in this lab, within the Target Group.

#### Target Group

A **Target Group** refers to a collection of AWS resource components that will receive and process data traffic routed through the Load Balancer.

In this exercise, our focus is on deploying the application through the Auto Scaling Group to ensure scalability as per user requirements. We will also implement a Load Balancer to efficiently manage load distribution and coordinate user access to our Application Tier.

Prior to proceeding, it is recommended that you thoroughly review the documentation titled "Deploying FCJ Management Applications on Windows/AmazonLinux Virtual Machines" to gain a clear understanding of deploying the application on a virtual machine. The FCJ Management deployed virtual machine will be utilized for extensive deployment and scaling within the Auto Scaling Group.

![Auto Scaling Group](/images/2-Prerequiste/0.png?featherlight=false&width=50pc)
