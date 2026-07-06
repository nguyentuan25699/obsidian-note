---
date: 2026-07-05
tags:
  - code
  - learning
  - js
draft: false
---
## 1. Introduction HTTP Module
- HTTP Module is a built in Node.js module that allows Node.js to transfer data over the Hypertext Transfer Protocol (HTTP).

## 2. Working with HTTP Module
### Node.js as a Web Server
- The HTTP module can create an HTTP server that listens to server ports and gives a response back to the client.
- Use the createServer() method to create an HTTP server:
```js
//create a server object:
http.createServer((request, response) => {

}); //the callback function is called the request handler
```

![[Pasted image 20260705140707.png]]



### Node.js as a Web Client
- To create Web Client, you can also use http Module

```js
const http = require('http');
var options = {
    host: 'localhost',
    port: '7000',
};

var callback = function(response) {
    var body = '';
    
    response.on('data', function(data) {
        body += data;
    });
    
    response.on('end', function() {
        console.log(body);
    });
};

var req = http.request(options, callback);

req.on('error', (e) => {
    console.error(`Problem with request: ${e.message}`);
});

req.end();
```

Run: node client.js
```sh
// Result
Hello, World
```

## 3. Introduction URL Module
- The url module provides utilities for URL resolution and parsing.
![[Pasted image 20260705141200.png]]

- Step 1: Include URL module 
	var url = require('url');
- Step 2 : Creates a new URLobject
	var q = new URL(address);
- Step 3: Set or get properties
- Run: node url_module.js

```js
var url = require('url');
var address = 'http://localhost:7000/index.php?type=page&action=update&id=5221';

var q = new URL(address);
console.log(q.host); //returns 'localhost:7000'
console.log(q.pathname); // returns '/index.php'
console.log(q.search); // Returns'?type=page&action=update&id=5221'

var params = new URLSearchParams(q.search);
console.log(params); // Returns URLSearchParams { 'type' => 'page', 'action' => 'update', 'id' => '5221' }

console.log(params.get('type')); // Returns page
console.log(params.get('action')); // Return update
console.log(params.get('id')); // Return 5221
```

