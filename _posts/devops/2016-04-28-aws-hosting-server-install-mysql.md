---
layout: post
comments: true
categories: devops
---


## How to install MySQL on an Amazon EC2 Server Instance?
Being a newbie to server administration especially with Linux, I found myself looking all over the internet on how to install a mysql server instance! Here is what worked for me on the Amazon EC2 instance:

## To install a MySQL Server

1. First step is to of course ssh into the EC2 instance
2. Then, at a command prompt, use the following command to install MySQL Server:

```sh
sudo yum install mysql-server
```
 When you are prompted, type 'y'.


## To start the installed MySQL Server
1. Start mysql, and configure it to start up automatically on reboot.

```sh
sudo chkconfig mysqld on

sudo service mysqld start
```
You would see a response like the following.

Starting mysqld


## Configuring newly installed MySQL Server
1. To update the password of root user do the following:

            mysqladmin -u root password [your_new_pwd]

2. To create a database do the following:
            mysqladmin -u root -p create [your_new_db]
When you are prompted for a password, type [your_new_pwd]. Well that's it. There rest of the MySQL functionality is as usual. For more details on other functionalities please use the MySQL website.


mysql -u root -p


## Using MySQL Externally
 1. If you need to access MySQL from another server, then you need to execute these following additional steps.
First off, create a MySQL user who can connect from any type of host using the following SQL:
    ```sh
    GRANT ALL PRIVILEGES ON *.* TO 'theuser'@'localhost'

    GRANT ALL PRIVILEGES ON *.* TO 'theuser'@'localhost'

    CREATE USER 'theuser'@'%' IDENTIFIED BY '[your_pwd]'

    GRANT ALL PRIVILEGES ON *.* TO 'theuser'@'%' WITH GRANT OPTION
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' identified by “yourpasswordhere”;
    ```



 2. Next, from the AWS Management Console find the Security Group that you assigned to your instance during set-up and add 'MySQL' to the group. You can also manually add port 3306. Save and whoala ready to go!


Source: [Link](http://text-analytics101.rxnlp.com/2013/11/how-to-install-mysql-on-amazon-ec2.html)