---
title : "Create DB Subnet Group"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 2.4 </b> "
---

#### Create DB Subnet Group


1. Go to **[RDS](https://ap-southeast-1.console.aws.amazon.com/rds/home?region=ap-southeast-1)**

   - Select **Subnet groups**
   - Select **Create DB subnet group**

![Create SG](/images/4/0001.png?featherlight=false&width=90pc)

2. In the **Create DB subnet group** interface

   - **Name**, enter **```FCJ-Management-Subnet-Group```**
   - **Description**, enter ```Subnet Group for FCJ Management```
   - Select the created VPC.

![Create SG](/images/4/0002.png?featherlight=false&width=90pc)

3. Configure **subnet**

   - Select the AZ
   - Select subnet
   - Select **Create**

![Create SG](/images/4/0003.png?featherlight=false&width=90pc)

4. Successfully create **DB Subnet Group**

![Create SG](/images/4/0004.png?featherlight=false&width=90pc)

![Create SG](/images/4/0005.png?featherlight=false&width=90pc)