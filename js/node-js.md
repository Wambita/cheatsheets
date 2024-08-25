
# **Node.js Cheatsheet**

## **1. Basics**

### **What is Node.js?**
- **Description:** Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine that allows you to run JavaScript on the server side.

### **Installing Node.js**
- **Description:** Download and install Node.js from [nodejs.org](https://nodejs.org/).

### **Node.js REPL (Read-Eval-Print Loop)**
- **Description:** An interactive shell to evaluate JavaScript expressions.
- **Example:**
  ```bash
  node
  > console.log("Hello, Node.js!");
  Hello, Node.js!
  ```

### **Basic File Execution**
- **Description:** Run a Node.js script from the command line.
- **Example:**
  ```bash
  node script.js
  ```

## **2. Core Modules**

### **File System (`fs`)**
- **Description:** Provides an API for interacting with the file system.
- **Example:**
  ```javascript
  const fs = require('fs');

  // Read a file
  fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
  });

  // Write to a file
  fs.writeFile('example.txt', 'Hello, Node.js!', (err) => {
    if (err) throw err;
    console.log('File has been saved!');
  });
  ```

### **HTTP**
- **Description:** Creates HTTP servers and clients.
- **Example:**
  ```javascript
  const http = require('http');

  const server = http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello, Node.js!\n');
  });

  server.listen(3000, '127.0.0.1', () => {
    console.log('Server running at http://127.0.0.1:3000/');
  });
  ```

### **Path**
- **Description:** Provides utilities for working with file and directory paths.
- **Example:**
  ```javascript
  const path = require('path');

  const filePath = path.join(__dirname, 'example.txt');
  console.log(filePath);
  ```

### **Events**
- **Description:** Provides a way to handle asynchronous events.
- **Example:**
  ```javascript
  const EventEmitter = require('events');
  const myEmitter = new EventEmitter();

  myEmitter.on('event', () => {
    console.log('An event occurred!');
  });

  myEmitter.emit('event');
  ```

## **3. Asynchronous Programming**

### **Callbacks**
- **Description:** Functions passed as arguments to be executed after an operation completes.
- **Example:**
  ```javascript
  function doSomething(callback) {
    setTimeout(() => {
      callback('Done!');
    }, 1000);
  }

  doSomething((message) => {
    console.log(message); // "Done!"
  });
  ```

### **Promises**
- **Description:** Represents the eventual completion (or failure) of an asynchronous operation.
- **Example:**
  ```javascript
  function doSomething() {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve('Done!');
      }, 1000);
    });
  }

  doSomething().then(message => {
    console.log(message); // "Done!"
  });
  ```

### **Async/Await**
- **Description:** Syntactic sugar for working with Promises, allowing asynchronous code to be written in a synchronous style.
- **Example:**
  ```javascript
  async function doSomething() {
    return 'Done!';
  }

  async function main() {
    const message = await doSomething();
    console.log(message); // "Done!"
  }

  main();
  ```

## **4. Express.js Framework**

### **Setting Up Express**
- **Description:** A minimal and flexible Node.js web application framework.
- **Example:**
  ```bash
  npm install express
  ```

### **Basic Express Server**
- **Description:** Create a simple web server with Express.
- **Example:**
  ```javascript
  const express = require('express');
  const app = express();

  app.get('/', (req, res) => {
    res.send('Hello, Express!');
  });

  app.listen(3000, () => {
    console.log('Server running at http://127.0.0.1:3000/');
  });
  ```

### **Middleware**
- **Description:** Functions that have access to the request, response, and the next middleware function in the application’s request-response cycle.
- **Example:**
  ```javascript
  app.use((req, res, next) => {
    console.log('Middleware executed!');
    next();
  });
  ```

## **5. Working with Databases**

### **MongoDB with Mongoose**
- **Description:** MongoDB is a NoSQL database, and Mongoose is an ODM (Object Data Modeling) library for MongoDB.
- **Example:**
  ```bash
  npm install mongoose
  ```

  ```javascript
  const mongoose = require('mongoose');

  mongoose.connect('mongodb://localhost/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true });

  const User = mongoose.model('User', new mongoose.Schema({
    name: String,
    age: Number
  }));

  const user = new User({ name: 'John Doe', age: 30 });
  user.save().then(() => console.log('User saved!'));
  ```

### **PostgreSQL with `pg`**
- **Description:** PostgreSQL is a relational database, and `pg` is a Node.js client for PostgreSQL.
- **Example:**
  ```bash
  npm install pg
  ```

  ```javascript
  const { Client } = require('pg');

  const client = new Client({
    user: 'yourusername',
    host: 'localhost',
    database: 'yourdatabase',
    password: 'yourpassword',
    port: 5432,
  });

  client.connect();

  client.query('SELECT NOW()', (err, res) => {
    console.log(err ? err.stack : res.rows[0]);
    client.end();
  });
  ```

## **6. Error Handling**

### **Try-Catch for Synchronous Code**
- **Description:** Handle errors in synchronous code using try-catch blocks.
- **Example:**
  ```javascript
  try {
    throw new Error('Something went wrong!');
  } catch (error) {
    console.error(error.message);
  }
  ```

### **Error Handling in Promises**
- **Description:** Handle errors in asynchronous code using `.catch()` method.
- **Example:**
  ```javascript
  function doSomething() {
    return new Promise((resolve, reject) => {
      reject(new Error('Something went wrong!'));
    });
  }

  doSomething().catch(error => {
    console.error(error.message);
  });
  ```

## **7. Packages and Modules**

### **npm (Node Package Manager)**
- **Description:** npm is the package manager for Node.js, used to install and manage packages.
- **Example:**
  ```bash
  # Initialize a new Node.js project
  npm init

  # Install a package
  npm install lodash

  # Use the package in your code
  const _ = require('lodash');
  console.log(_.random(1, 100)); // Random number between 1 and 100
  ```

### **CommonJS Modules**
- **Description:** The module system used by default in Node.js.
- **Example:**
  ```javascript
  // module.js
  module.exports = function() {
    return 'Hello from module!';
  };

  // main.js
  const greet = require('./module');
  console.log(greet()); // "Hello from module!"
  ```

### **ES Modules**
- **Description:** JavaScript modules standard, supported in modern Node.js versions with the `.mjs` extension or `"type": "module"` in `package.json`.
- **Example:**
  ```javascript
  // module.mjs
  export function greet() {
    return 'Hello from ES module!';
  }

  // main.mjs
  import { greet } from './module.mjs';
  console.log(greet()); // "Hello from ES module!"
  ```
