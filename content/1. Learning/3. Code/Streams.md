---
date: 2026-07-05
tags:
  - js
  - code
  - learning
draft: false
---
## 1. What are Streams?
- Streams are collections of data — just like arrays or strings.
- The difference is that streams might not be available all at once, and they don’t have to fit in memory. This makes streams really powerful when working with large amounts of data, or data that’s coming from an external source one chunk at a time.
- What makes streams unique, is that instead of a program reading a file into memory all at once like in the traditional way, streams read chunks of data piece by piece, processing its content without keeping it all in memory.
![[Pasted image 20260705145718.png]]

___

## 2. Why use Streams?
- Streams basically provide two major advantages compared to other data handling methods:
	- Memory efficiency: you don’t need to load large amounts of data in memory before you are able to process it.
	- Time efficiency: it takes significantly less time to start processing data as soon as you have it, rather than having to wait with processing until the entire payload has been transmitted.

___

## 3. Streams in Node.js
**There are 4 types of streams in Node.js**

- **Writable**: streams to which we can write data. For example, fs.createWriteStream() lets us write data to a file using streams.
- **Readable**: streams from which data can be read. For example: fs.createReadStream() lets us read the contents of a file.
- **Duplex**: streams that are both Readable and Writable. For example, net.Socket
- **Transform**: streams that can modify or transform the data as it is written and read. For example, in the instance of file-compression, you can write compressed data and read decompress data to and from a file.

Each type of Stream is an EventEmitter instance and throws several events at different instance of times. For example, some of the commonly used events are:
- **data** − This event is fired when there is data is available to read.
- **end** − This event is fired when there is no more data to read.
- **error** − This event is fired when there is any error receiving or writing data.
- **finish** − This event is fired when all the data has been flushed to under lying system.


## 4. Working with Node.js Streams
### Reading from a Stream
- Step 1: Create a text file named input.txt having the content “Node.js - Streams (Sun*)"
- Step 2: Create a readable stream to read file
```js
var fs = require('fs');
var data = ''; 

// Create a readable stream
var readerStream = fs.createReadStream('input.txt'); 

// Set the encoding to be utf8.
readerStream.setEncoding('UTF8'); 

// Handle stream events --> data, end, and error
readerStream.on('data', function(chunk) {
    data += chunk;
});

readerStream.on('end', function() {
    console.log(data);
});

readerStream.on('error', function(err) {
    console.log(err.stack);
});

console.log('Program Ended');
```

Run: node streams.js
```sh
// Result
Program Ended
Node.js - Stream (Sun*)
```


### Writing to a Stream
- Create a writable stream with text "Node.js - Write stream(Sun*)"
```js
var fs = require('fs');
var data = 'Node.js - Write stream (Sun*)';

// Create a writable stream
var writerStream = fs.createWriteStream('output.txt');

// Write the data to stream with encoding to be utf8
writerStream.write(data, 'UTF8');

// Mark the end of file
writerStream.end(); 

// Handle stream events --> finish, and error
writerStream.on('finish', function() {
    console.log('Write completed. output.text created inyour current directory');
});

writerStream.on('error', function(err) {
    console.log(err.stack);
});

console.log('Program Ended');
```

- Run: node write_stream.js
```sh
// Result
Program Ended
Write completed. output.text
created in your current directory
```


## References
  
- https://nodejs.dev/learn/nodejs-streams
- https://nodejs.org/api/stream.html
- https://nodesource.com/blog/understanding-streams-in-nodejs