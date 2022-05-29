---
title : "Deploying FCJ Management Application"
date : "`r Sys.Date()`"
weight : 9
chapter : false
pre : " <b>2.9 </b> "
---

#### Deploy FCJ Management application

1. We use git to clone the source code. First of all, install git with the following command:

```
sudo yum install git
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0001-deployapp.png?featherlight=false&width=90pc)

2. Use the git init command used to create, and initialize a new Git repository (Git Repo) locally.

```
git init
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0002-deployapp.png?featherlight=false&width=90pc)

3. Implement the application code repository clone

```
git clone https://github.com/First-Cloud-Journey/000004-EC2.git
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0003-deployapp.png?featherlight=false&width=90pc)

4. Go to the directory of the lab 000004-EC2

```
cd 000004-EC2
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0004-deployapp.png?featherlight=false&width=90pc)

5. NPM stands for Node package manager and is a tool to create and manage Javascript programming libraries for Node.js. Using npm init to initialize the project will generate a sample package.json file.

```
npm init

```

- If you do not have Nodejs installed, you can refer to [Install Nodejs on Amazon Linux](https://000004.awsstudygroup.com/en/6-awsfcjmanagement-linux/6.2-setupnodejsonec2linux/)

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0005-deployapp.png?featherlight=false&width=90pc)

6. Next we do the dependencies installation

- express
- Dotenv
- express-handlebars
- body-parser
- Mysql

```
npm install express dotenv express-handlebars body-parser mysql
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0006-deployapp.png?featherlight=false&width=90pc)

7. Perform the test and create a **.env** file using **vi** to configure the database.

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0007-deployapp.png?featherlight=false&width=90pc)

8. Perform database configuration

```
DB_HOST = 'db-instance.crmmitoajvxx.us-east-1.rds.amazonaws.com'
DB_NAME = 'awsuser'
DB_USER = 'admin'
DB_PASS = '123Vodanhphai'
```

- In which, DB_HOST is the Endpoint of the DB instance
- DB_NAME is the name of the database created in the DB instance
- DB_USER is the database username that was created in the DB instance
- DB_PASS is the database password that was created in the DB instance

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0008-deployapp.png?featherlight=false&width=90pc)

9. Restart the Express server. Use Nodemon to save time

```
npm install --save-dev nodemon
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/0009-deployapp.png?featherlight=false&width=90pc)

10. Start the local server

```
npm start
```

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/00010-deployapp.png?featherlight=false&width=90pc)

11. Access to **EC2**

- Select **Instances**
- Select **FCJ-Management** instance
- Copy **Public IPv4 address**

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/00011-deployapp.png?featherlight=false&width=90pc)

12. Use a browser and paste **Public IPv4 address** to test the application.

![Deploy app](/images/2-Prerequiste/2.9-Deployapp/00012-deployapp.png?featherlight=false&width=90pc)