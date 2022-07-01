# MEAN STACK DEPLOYMENT TO UBUNTU IN AWS#

## Mean stack is a combination of the following components ##

1. MongoDB (Document database) – Stores and allows to retrieve data.
2. Express (Back-end application framework) – Makes requests to Database for Reads and Writes
3. Angular (Front-end application framework) – Handles Client and Server Requests
4. Node.js (JavaScript runtime environment) – Accepts requests and displays results to end user

In order to complete this project you will need an AWS account and a virtual server with Ubuntu Server OS.

we would be implementing a Simple Book Register web form using MEAN stack.

## Step 1: Install NodeJs

Update Ubuntu 

``` sudo apt update```

Upgrade Ubuntu

``` sudo apt Upgrade ```

Add Certficates

```sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates ```

```sudo npm install body-parser ```

**Install NodeJs

```sudo apt install -y nodejs```

after installing our NodeJs Server we move to the next step 

## Step 2:Install MongoDB ##

MongoDB stores data in flexible, JSON-like documents. Fields in a database can vary from document to document and data structure can be changed over time

``` sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 ```

```echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list ```

**Install MongoDB**

``` sudo apt install -y mongodb ```

Start The server

``` sudo service mongodb start ```

Verify that the service is up and running

```sudo systemctl status mongodb ```

Install npm – Node package manager.

```sudo apt install -y npm```

Install body-parser package


We need ‘body-parser’ package to help us process JSON files passed in requests to the server.

```sudo npm install body-parser ```

we need to create a book folder to keep our repositories

```mkdir Books && cd Book```

we need to initialize npm project

npm init

Add a file to it named server.js

```vi server.js```

Copy and paste the web server code below into the server.js file.

```var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port')); ```
    
    
});




