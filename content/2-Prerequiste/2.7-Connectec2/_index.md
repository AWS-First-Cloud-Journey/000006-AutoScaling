---
title : "Connecting EC2 instances"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 2.7 </b> "
---

#### Connect EC2 instance

1. Use **MobaXterm** to SSH into the instance via port 22.

- Select **Session**

![Connect EC2 instance](/images/2-Prerequiste/2.7-Connectec2/0001-connectec2.png?featherlight=false&width=90pc)

2. In the **Session settings** section,

- **Remote host**, enter **Public IPv4 address** of the instance
- **Specify username**, enter **ec2-user**
- Check port 22
- Select **Advanced SSH settings**
- Select **Use private key** and select **keypair** of the instance.
- Select **OK**

![Connect EC2 instance](/images/2-Prerequiste/2.7-Connectec2/0002-connectec2.png?featherlight=false&width=90pc)

3. EC2 instance connection is successful.

![Connect EC2 instance](/images/2-Prerequiste/2.7-Connectec2/0003-connectec2.png?featherlight=false&width=90pc)


You can refer to [How to install Nodejs on EC2](https://000004.awsstudygroup.com/en/6-awsfcjmanagement-linux/6.2-setupnodejsonec2linux/)

4. Install node version manager (nvm) ) by typing the following in the following command line:


```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
```

![Connect EC2 instance](/images/2-Prerequiste/2.7-Connectec2/0004-connectec2.png?featherlight=false&width=90pc)

5. Enable nvm by typing the following in the command line and Use nvm to install the latest version of Node.js by typing the following in the command line.

```
. ~/.nvm/nvm.sh
nvm install 16
```

![Connect EC2 instance](/images/2-Prerequiste/2.7-Connectec2/0005-connectec2.png?featherlight=false&width=90pc)

6. Test installed nodejs successfully

```
node -v
npm -v
```

![Connect EC2 instance](/images/2-Prerequiste/2.7-Connectec2/0006-connectec2.png?featherlight=false&width=90pc)
