# SIMPLE TO-DO APPLICATION ON MERN WEB STACK Project 3
this Mern stack comprises of the following
1. MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

2. ExpressJS: A server side Web Application framework for Node.js.

3. ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

4. Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

## Step 0- Spin up a a virtual server with Ubuntu Server OS on AWS 
Having spin up and running a virtual server (EC2) the next step is to configure our backend 

## STEP 1 – BACKEND CONFIGURATION

Update ubuntu **sudo apt update**

Upgrade ubuntu **sudo apt upgrade**

Get the location of Node.js software from Ubuntu repositories. **curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -**

Install Node.js with the command below **sudo apt-get install -y nodejs**

Verify the node installation with the command _**node -v**_  and Verify the node installation with the command _**npm -v**_

## Next is the Application Code Set Up

Create a new directory for your To-Do project by running mkdir Todo and verify it was created _ls_

Initialize your project using _npm init_ and run _ls_ to verify you have package.json file created.

<img width="690" alt="npm-init" src="https://user-images.githubusercontent.com/101952842/171905149-c0989313-8f9c-4970-835b-0e931af26e6b.png">

## INSTALL EXPRESSJS

To use express, install it using npm: npm install express

Create a file index.js: touch index.js: and run ls: to confirm it was created.

Install the dotenv module: npm install dotenv

Open the index.js file: vim index.js

Type the code below into it and save:


const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
