# SIMPLE TO-DO APPLICATION ON MERN WEB STACK Project 3
this Mern stack comprises of the following
1. MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

2. ExpressJS: A server side Web Application framework for Node.js.

3. ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

4. Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

## Step 0- Spin up a a virtual server with Ubuntu Server OS on AWS 
Having spin up and running a virtual server (EC2) the next step is to configure our backend 

## STEP 1 – BACKEND CONFIGURATION
The Ubuntu server was apt updated and Upgrades, after which the location of the node servers were located on UBuntu respositories and was installed using the below codes 
sudo apt-get install -y nodejs
next is  Application Code Setup
Create a new directory for your To-Do project: using the commands mkdir Todo after which you change into the directory and 
Next, you will use the command npm init to initialise your project, so that a new file named package.json will be created. This file will normally contain information about your application and the dependencies that it needs to run. Follow the prompts after running the command. You can press Enter several times to accept default values, then accept to write out the package.json file by typing yes. 

Having done all of that Next, we will Install ExpressJs and create the Routes directory.
**INSTALL EXPRESSJS**
Remember that Express is a framework for Node.js, therefore a lot of things developers would have programmed is already taken care of out of the box. Therefore it simplifies development, and abstracts a lot of low level details. For example, Express helps to define routes of your application based on HTTP methods and URLs.
To use express, install it using npm:
npm install express
Now create a file index.js with this command touch index.js

