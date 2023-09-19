---
title : "Create Target Group"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

#### Create Target Group

1. Access **EC2** interface:
   - Select **Target Groups**
   - Select **Create target group**

![Deploy app](/images/14/0001.png?featherlight=false&width=90pc)

2. Make a configuration:
   - Select **Instances**

![Deploy app](/images/14/0002.png?featherlight=false&width=90pc)

3. On the **Specify group details** page, set the following parameters for **target group**:
   - **Target group name**: Enter the name of the target group (e.g., **FCJ-Management-TG**).
   - **Protocol**: HTTP.
   - **Port**: **5000** (Port used by FCJ Management).
   - Leave the remaining items as default.

![Deploy app](/images/14/0003.png?featherlight=false&width=90pc)

4. Select **Next**

![Deploy app](/images/14/0004.png?featherlight=false&width=90pc)

5. In the **Available instances** interface:
   - Select **FCJ-Management** instance
   - Select port **5000**
   - Select **Include as pending below** (if not selected, accessing with DNS Load Balancer may result in an **HTTP 503: Service unavailable** error)
   - Review
   - Select **Create target group**

![Deploy app](/images/14/0005.png?featherlight=false&width=90pc)

6. In the **Register pending targets only** interface, select **Continue**

![Deploy app](/images/14/0006.png?featherlight=false&width=90pc)

7. Finish creating the **Target group**

![Deploy app](/images/14/0007.png?featherlight=false&width=90pc)
