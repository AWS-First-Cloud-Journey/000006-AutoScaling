---
title : "Launch Template"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

#### Launch Template

In this section, you will create a Launch Template using the AMI you created from the Amazon Linux 2 Instance in the previous step.

1. Access to **EC2**

   - Select **Launch Templates**
   - Select **Create launch template**

![Deploy app](/images/13/0001.png?featherlight=false&width=90pc)

2. In the **Create launch template** interface

    - **Launch template name**, enter **```FCJ-Management-template```**
    - **Template version description**, enter **```Template for FCJ Management```**

![Deploy app](/images/13/0002.png?featherlight=false&width=90pc)

3. Perform **AMI** selection

   - Select **My AMIs**
   - Select **Owned by me**
   - Select **FCJ-Management-AMI**

![Deploy app](/images/13/0003.png?featherlight=false&width=90pc)

4. Make **Instance type** selection

   - Select **t2.micro**
   - **Key pair**, select **aws-fcj-key** created when creating **EC2** instance.

![Deploy app](/images/13/0004.png?featherlight=false&width=90pc)

5. Configure **Network**

   - **Subnet**, select **public subnet**
   - **Firewall (Security Group)**, select **Select existing security group**
   - Select **FCJ-Management-SG**

![Deploy app](/images/13/0005.png?featherlight=false&width=90pc)

6. Check again and execute **Create launch template**

![Deploy app](/images/13/0006.png?featherlight=false&width=90pc)

7. Execute successfully and select **View launch templates**

![Deploy app](/images/13/0007.png?featherlight=false&width=90pc)

8. View the template just created.

![Deploy app](/images/13/0008.png?featherlight=false&width=90pc)