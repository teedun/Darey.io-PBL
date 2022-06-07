# **WEB STACK IMPLEMENTATION (LEMP STACK)**
## STEP 1 – INSTALLING THE NGINX WEB SERVER
In order to display web pages to our site visitors, we are going to employ Nginx, a high-performance web server. We’ll use the apt package manager to install this package.
Since this is our first time using apt for this session, start off by updating your server’s package index. Following that, you can use apt install to get Nginx installed:

![ngnix  installed](https://user-images.githubusercontent.com/101952842/161452327-00fd0817-8414-4946-8a6e-012e6a8fd538.png)

we need to add a rule to EC2 configuration to open inbound connection through port 80: this is to make the website accessible on the internet 

## STEP 2 — INSTALLING MYSQL

Now that you have a web server up and running, you need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database. MySQL is a popular relational database management system used within PHP environments, so we will use it in our project.

 _*apt*_ command will be use to acquire and install this software
 
![mysql installed ](https://user-images.githubusercontent.com/101952842/161453181-f2d20e36-e94e-4189-bd59-2f97c1c63328.png)

A secure installation was done and validate password plugin was configured

## STEP 3 – INSTALLING PHP

Having set up Nginx to serve as the content and MySQL to store and manage  data. Now that PHP is installed, you can use it to process code and generate dynamic content for the web server.

Unlike Apache, which embeds the PHP interpreter in each request, Nginx requires an external programme to handle PHP processing and serve as a bridge between the PHP interpreter and the web server. This improves overall performance in most PHP-based websites, but it necessitates additional configuration. 

Install php-fpm, which stands for "PHP fastCGI process manager," and instruct Nginx to forward PHP requests to this software for processing. 

You'll also need php-mysql, a PHP module that allows PHP to communicate with MySQL databases. 

The core PHP packages will be installed automatically be installed as dependencies.

## STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR

When using the Nginx web server, we can create server blocks (similar to virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server. In this guide, we will use projectLEMP as an example domain name.

On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at 
/var/www/html. 

While this works well for a single site, it can become difficult to manage if you are hosting multiple sites. Instead of modifying /var/www/html, we’ll create a directory structure within /var/www for the your_domain website, leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites.

Create the root web directory for your_domain as follows:

sudo mkdir /var/www/projectLEMP

Next, we would assign ownership of the directory with the $USER environment variable, which will reference your current system user:

sudo chown -R $USER:$USER /var/www/projectLEMP

the file was edited using NANO Editor

Although your new website is now operational, the web root /var/www/projectLEMP remains empty. an index.html file was created in that location so that we can verify that your new server block is functioning properly

![LEmp installed](https://user-images.githubusercontent.com/101952842/161453500-44ba2114-465d-42db-8050-2b0e02f534bc.png)

## STEP 5 – TESTING PHP WITH NGINX

Our LAMP stack is completely installed and fully operational.

You can test it to validate that Nginx can correctly hand .php files off to your PHP processor.

this was done by creating a test PHP file in your document root. Open a new file called info.php within your document root in your text editor using the below command

sudo nano /var/www/projectLEMP/info.php 

in the Nano editor Type or paste the following lines into the new file. This is valid PHP code that will return information about your server:
<?php
phpinfo();

we can access this on the website and we would see a web page containing detailed information about your server:
a web page containing detailed information about your server:

![PHP info page](https://user-images.githubusercontent.com/101952842/161454102-c95cbcf2-955b-44ec-83d3-1ad1a930a94d.png)

## STEP 6 – RETRIEVING DATA FROM MYSQL DATABASE WITH PHP

 A test database (DB) with simple "To do list" and configure access to it, so the Nginx website would be able to query data from the DB and display it.
Firstly, i connect to the MYSQL console using the root account and created a database and  new user with password and grant the user all permissions

Next, we’ll create a test table named todo_list. From the MySQL console, run the following statement:

CREATE TABLE example_database.todo_list (
mysql>     item_id INT AUTO_INCREMENT,
mysql>     content VARCHAR(255),
mysql>     PRIMARY KEY(item_id)

A to do list was created in the database and run to test our database.

![todo list](https://user-images.githubusercontent.com/101952842/161454509-bcc89114-2228-47d1-8134-78443a41fbab.png)

![image](https://user-images.githubusercontent.com/101952842/161454693-46cc3427-16ae-4564-b0f5-07cbd64b331c.png)
