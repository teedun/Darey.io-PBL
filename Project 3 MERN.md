# SIMPLE TO-DO APPLICATION ON MERN WEB STACK Project 3

This Mern stack comprises of the following

1. MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

2. ExpressJS: A server side Web Application framework for Node.js.

3. ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

4. Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.

## Step 0- Spin up a a virtual server with Ubuntu Server OS on AWS 

Having spin up and running a virtual server (EC2) the next step is to configure our backend 

## STEP 1 – BACKEND CONFIGURATION

Update ubuntu  

``` 
sudo apt update 
```

Upgrade ubuntu  

``` 
sudo apt upgrade
 ```

Get the location of Node.js software from Ubuntu repositories. 

```
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```

Install Node.js with the command below 

```
sudo apt-get install -y nodejs
```

Verify the node installation with the command node    ```-v ```  and 

Verify the node installation with the command    ```npm -v ```


## Next is the Application Code Set Up

Create a new directory for your To-Do project by running mkdir Todo and verify it was created 

```
mkdir Todo 
```

and verify it was created 

```
ls
```

Initialize your project using 
```npm init``` and run ```ls```  to verify you have **package.json** file created.

<img width="690" alt="npm-init" src="https://user-images.githubusercontent.com/101952842/171905149-c0989313-8f9c-4970-835b-0e931af26e6b.png">

## INSTALL EXPRESSJS

To use express, install it using npm: npm install express

Create a file index.js: 

```
touch index.js:
```

and run ```ls``` to confirm it was created.

Install the dotenv module:

```
npm install dotenv
```

Open the index.js file: ```vim index.js```

Type the code below into it and save:

```
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

```
Notice that we have specified to use port 5000 in the code. This will be required later when we go on the browser.

Use :w to save in vim and use :qa to exit vim

Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:

```
node index.js
```
If every thing goes well, you should see Server running on port 5000 in your terminal.

![image](https://user-images.githubusercontent.com/101952842/172445471-5488dafb-033e-4080-bbd7-8fe93b5b06cb.png)

we need to open this port in EC2 Security Groups  port:5000 on AWS

![image](https://user-images.githubusercontent.com/101952842/172445766-c6616b2f-5812-41f4-821f-569c516049fe.png)

Open up your browser and try to access your server’s Public IP or Public DNS name followed by port 5000:

```
http://<PublicIP-or-PublicDNS>:5000
  ```
![image](https://user-images.githubusercontent.com/101952842/172445965-1049eedb-ab2c-4516-9879-4bbd6b311f76.png)

**Routes**

There are three actions that our To-Do application needs to be able to do:

Create a new task

Display list of all tasks

Delete a completed task

Each task will be associated with some particular endpoint and will use different standard HTTP request methods: POST, GET, DELETE.

For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes

```
mkdir route
```
```
cd routes
```

Now, create a file api.js with the command below

```
touch api.js
```

Open the file with the command below

```
vim api.js
```
Copy below code in the file.

```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```
we need to create a model.

A model is at the heart of JavaScript based applications, and it is what makes it interactive. We will also use models to define the database schema

Change directory back Todo folder with cd .. and install Mongoose

```
npm install mongoose
```

Create a new folder models :

```
mkdir models

```
Change directory into the newly created ‘models’ folder with

```
cd models
```

Inside the models folder, create a file and name it todo.js

```
touh todo.js
```

Open the file created with ``` vim todo.js ``` then paste the code below in the file:

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

```

Now we need to update our routes from the file api.js in ‘routes’ directory to make use of the new model.

In Routes directory, open api.js with vim api.js, delete the code inside with :%d command and paste there code below into it then save and exit

```
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;
```

We need a database where we would store all our data. Sign up here 

```
https://www.mongodb.com/atlas-signup-from-mlab
```

![image](https://user-images.githubusercontent.com/101952842/172459068-6a69a60a-d26b-4ccb-94f0-6e251fa3d02e.png)

allow access from anywhere into the database

Create a file in your Todo directory and name it .env.

```
touch .env
vi .env
```

Add the connection string to access the database in it, just as below:

```
DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
```

Ensure to update <username>, <password>, <network-address> and <database> according to your setup
  
Now we must update **index.js** to reflect the use of.env in order for Node.js to connect to the database.
  
Simply delete the file's existing content and replace it with the entire code below.
  
To do so with vim, follow the steps below.
  
Use **vim index.js** to open the file.
  
Type: press esc
  
Enter the percentage d
  
Press the 'Enter' key.
  
The entire content will be deleted, and then press I to enter vim's insert mode.
  
Now, paste the following code into the file.
  
  ```
  const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
  ```
  
  Start your server using the command:

  ```
node index.js
  ```
  
  Test the API using POSTMAN
  
  
  ## STEP 2 – FRONTEND CREATION ##
  
  In the same root directory as your backend code, which is the Todo directory, run:

 ```
 npx create-react-app client
  ```
  
  Running a React App
  
Before testing the react app, there are some dependencies that need to be installed.

Install concurrently. It is used to run more than one command simultaneously from the same terminal window.
  
  ```
npm install concurrently --save-dev
  ```
  
Install nodemon. It is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes.
  
  ```
npm install nodemon --save-dev
  ```
  
In Todo folder open the package.json file. Change the highlighted part of the below screenshot and replace with the code below.
  
  ```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
  ```
  
  ![image](https://user-images.githubusercontent.com/101952842/172461712-a0ea696a-19c2-4be4-816a-52e8a5e15fff.png)
  
  
  Configure Proxy in package.json
  
Change directory to ‘client’
  
cd client
  
Open the **package.json file
  
  ```
vi package.json
  ```
  
Add the key value pair in the package.json file "proxy": "http://localhost:5000".
  
The whole purpose of adding the proxy configuration in number 3 above is to make it possible to access the application directly from the browser by simply calling the server url like http://localhost:5000 rather than always including the entire path like http://localhost:5000/api/todos

Now, ensure you are inside the Todo directory, and simply do:

  ```
npm run dev
  ```
  
Your app should open and start running on localhost:3000
  
  **Creating your React Components**
  
  From your Todo directory run

  ```
cd client
  ```
  
move to the src directory

  ```
cd src
  ```
  
Inside your src folder create another folder called components

  ```
mkdir components
  ```
  
Move into the components directory with
  
```
cd components
  ```
  
Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js.

  ```
touch Input.js ListTodo.js Todo.js
  ```
  
Open Input.js file
  
  ```
vi Input.js
  ```
  
Copy and paste the following
  
  ```
  import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
  ```
  To make use of Axios, which is a Promise based HTTP client for the browser and node.js, you need to cd into your client from your terminal and run yarn add axios or npm install axios.
  
  Install Axios
  
```
npm install axios
  ```
  
  Go to ‘components’ directory

  ```
cd src/components
  ```
  
After that open your ListTodo.js
  
```
vi ListTodo.js
  ```
  
in the ListTodo.js copy and paste the following code
  
  ```
  import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

return (
<ul>
{
todos &&
todos.length > 0 ?
(
todos.map(todo => {
return (
<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
)
})
)
:
(
<li>No todo(s) left</li>
)
}
</ul>
)
}

export default ListTodo
  ```
  
  Then in your Todo.js file you write the following code
  
  ```
  import React, {Component} from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {

state = {
todos: []
}

componentDidMount(){
this.getTodos();
}

getTodos = () => {
axios.get('/api/todos')
.then(res => {
if(res.data){
this.setState({
todos: res.data
})
}
})
.catch(err => console.log(err))
}

deleteTodo = (id) => {

    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if(res.data){
          this.getTodos()
        }
      })
      .catch(err => console.log(err))

}

render() {
let { todos } = this.state;

    return(
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos}/>
        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
      </div>
    )

}
}

export default Todo;
  ```
  
  Make sure that you are in the src folder and run
  
```
vi App.js
  ```
  
Copy and paste the code below into it
  
  ```
  import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}

export default App;
  ```
  
  In the src directory open the App.css

  ```
vi App.css
  ```
  
Then paste the following code into App.css:
  
  ```
  .App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
  ```
  
  Exit

In the src directory open the index.css
  
```
vim index.css
  ```
  
  Copy and paste the code below:
  
  ```
  body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}
  ```
  
  Go to the Todo directory

 ```
cd ../..
  ```
  
When you are in the Todo directory run:

  ```
npm run dev
  ```
  
  ![image](https://user-images.githubusercontent.com/101952842/172464234-427766dd-55c0-4204-b511-f9fd35ceee71.png)
  

  **END**

  
  
  
  
