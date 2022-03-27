# LAMP STACK IMPLEMENTATION
## STEP 1 — INSTALLING APACHE AND UPDATING THE FIREWALL
After launching an EC2 Instance with Ubuntu OS, I SSH into the Instance using Mobaxterm.
![SSH into instance LAmp](https://user-images.githubusercontent.com/101952842/160261960-25f61b13-9684-4412-8b36-e51d8893f2bd.png)

I proceeded to install Apache and upgrade the firewall.

The most popular web server software is Apache HTTP Server. Apache is a free open source software developed and maintained by the Apache Software Foundation. I install Apache using Ubuntu's package manager Apt and verify that it is running as a service in my operating system, and I open TCP port 80 to allow web browsers to access my newly created Web page.

![Apache2 screen](https://user-images.githubusercontent.com/101952842/160262198-7460b6f5-dbf0-4af4-8b69-179baa69715f.png)


## STEP 2 — INSTALLING MYSQL
The next is to install a database Management System (DBMS) this is to enable to store and amanage data for the website in a relational database. MySQL is a popular relational database management system used within PHP environments.


## STEP 3 — INSTALLING PHP
MySQL server is now up and running and secure. The final component of the LAMP stack will be installed next PHP 

PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. A vitual Hosdt forthe website using apache2 was created 

## STEP 4 — CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

A domain called project lamp was created

![hello lamp page](https://user-images.githubusercontent.com/101952842/160262389-9a90efca-ee3b-495a-96b9-e0987552bb5d.png)

## STEP 5 — ENABLE PHP ON THE WEBSITE

Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server.

Now that you have a custom location to host your website’s files and folders, we’ll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

![php page ](https://user-images.githubusercontent.com/101952842/160262554-c864341c-86fb-4500-9b82-cf0ad0e26afb.png)
