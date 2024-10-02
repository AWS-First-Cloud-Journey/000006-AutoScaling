---
title: "Introduction"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<strong>1. </strong>"
---

#### Introduce

In this exercise, we will be deploying the application using an Auto Scaling Group to ensure the application's scalability based on user demand. Additionally, we will implement a Load Balancer to distribute the load and manage user access requests to our Application Tier.

Before proceeding, please review the document [Deploying FCJ Management Application on a Windows/AmazonLinux Virtual Machine] to understand how to deploy the application on a virtual machine. We will utilize the virtual machine where **FCJ Management** is deployed for the purpose of mass deployment and scaling within the Auto Scaling Group.

#### Auto Scaling Group
1. Why Use Auto Scaling Group? 
   
   When our application goes live, the volume of users accessing it will change over time. Therefore, we need to frequently adjust (scale) the number of instances to enhance availability and save costs. To automate and make scaling flexible, we have a solution known as the Auto Scaling Group.
2. Overview of Auto Scaling Group
   
    **Auto Scaling Group (ASG)** helps automatically adjust the number of EC2 instances based on the needs of the application. ASG can automatically scale up when traffic increases or scale down when traffic decreases, optimizing resources and reducing costs. It also ensures high availability by distributing instances across multiple Availability Zones to maintain continuous operation even if part of the system encounters issues.
3. Types of Scaling in ASG
   
   In this content, we will explore the following types of scaling:
   - **Manual Scaling**: Users manually adjust the number of EC2 instances in the Auto Scaling Group based on demand. This is a manual method that does not automatically respond to specific metrics.
   - **Dynamic Scaling**: Automatically adjusts the number of instances based on real-time metrics such as CPU utilization, network traffic, or custom metrics from CloudWatch. Dynamic scaling has three primary policies: **Target Tracking Scaling**, **Step Scaling**, **Simple Scaling**.
   - **Scheduled Scaling**: Allows us to configure specific times to automatically scale up or down instances, for example, increasing the number of instances during peak hours or decreasing them outside of working hours. This is suitable for scenarios where we already know the traffic pattern.
   - **Predictive Scaling**: It predicts activity by analyzing historical load data to identify daily or weekly patterns in traffic flow. It uses this information to forecast future capacity needs, allowing Amazon EC2 Auto Scaling to proactively increase the capacity of the Auto Scaling group as needed.

#### Launch Template

**Launch Template** is a configuration that contains the necessary parameters to launch EC2 instances. It stores details such as instance type, AMI (Amazon Machine Image), key pair, network settings, security groups, and other configuration information for EC2. This simplifies the instance creation process and supports the automatic creation of new instances in ASG.

#### Elastic Load Balancer

**Elastic Load Balancer** is a tool that helps evenly distribute workloads (traffic) to multiple servers or instances to ensure stable system operation and prevent any single server from becoming overloaded. It optimizes performance, increases availability, and ensures that if one server encounters issues, traffic will be redirected to other servers without affecting users.

#### Target Group

**Target Group**  is a component of the Elastic Load Balancer (ELB) that is used to identify and manage the EC2 instances that the Load Balancer will distribute traffic to.