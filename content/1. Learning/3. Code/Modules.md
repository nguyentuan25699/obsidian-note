---
date: 2026-07-05
tags:
  - code
  - learning
  - js
draft: false
---
## 1. introduction
- **Module** is a simple or complex functionality organized is single or multiple JavaScript files which can be reused throughout the Node.js application.
- Each module in Node.js has its own contex
	- Cannot interfere with other modules or pollute global scope
	- Can be placed in a separate .js file under a separate folder.

## 2. Node.js Module Types
- Node.js includes three types of modules: 
	- Core Modules
	- Local Modules
	- 3rd Modules

### Core Modules
- The core modules include bare minimum functionalities of Node.js
- These core modules are complied into its binary distribution and load automatically when Node.js process starts
- Import the core module first in order to use it in your application.

### Loading Core Modules
- In order to use Node.js or NPM modules, you first need to import it using **require()** function as shown below.
```js
var module = require("module_name")
```

- The require() function will  return object, function, property or any other JavaScript type, depending on what the specified module returns

### Node.js Local Module
- Local modules are modules created locally in your Node.js application
- These modules include different functionalities of your application in separate files and folders
- You can also package it and distribute it via NPM, so that Node.js community can use it

```js
exports.add = function (x, y) {
	return x + y;
};	

exports.sub = function (x, y) {
	return x - y;
};

exports.mult = function (x, y) {
	return x * y;
};

exports.div = function (x, y) {
	return x / y;
};
```


```js
var calculator = require('./calc');

var x = 50, y = 20;

console.log(calculator.add(x, y));

console.log(calculator.sub(x, y));

console.log(calculator.mult(x, y));

console.log(calculator.div(x, y));
```


### Node.js 3rd Module
- Third-party modules are modules that are available online using the Node PackageManager(NPM)
- It can be installed in the project folder  or globally

## 3. Export Module in Node.js
- The module.exports is a special object which is included in every JavaScript file in the Node.js application by default
- The module is a variable that represents the current module, and exports is an object that will be exposed as a module.So, whatever you assign to module.exports will be exposed as a module.
### Export Literals
- exports is an object. So it exposes whatever you assigned to it as a module.For example, if you assign a string literal then it will expose that string literal as a module.

```js
// Message.js
module.exports = 'Hello world';

// app.js
var msg = require('./Messages.js');

console.log(msg);
```

### Export Object
- The exports is an object. So, you can attach properties or methods to it. The following example exposes an object with a string property in Message.js file.

```js
// Message.js
exports.SimpleMessage = 'Hello world ';

//or
module.exports.SimpleMessage = 'Helloworld';

// app.js
var msg = require('./Messages.js ');

console. log(msg.SimpleMessage);
```


### Export Function
- You can attach an anonymous function to exports object.

```js
// Log.js
module.exports = function (msg) {
	console.log(msg);
};

// app.js
var msg = require('./Log.js');

msg('Hello World');
```


### Export Function as a Class
- In JavaScript, a function can be treated like a class. The following example exposes a function that can be used like a class.
```js
// Person.js
module.exports = function (firstName, lastName) {
	this.firstName = firstName;
	this.lastName = lastName;
	this.fullName = function () {
		return this.firstName + ' ' + this.lastName;
	}
}

// app.js
var person = require('./Person.js');

var person1 = new person('James', 'Bond');

console.log(person1.fullName());
```

## References

- https://www.tutorialsteacher.com/nodejs/nodejs-module-exports
- https://www.w3schools.com/nodejs/nodejs_modules.asp
