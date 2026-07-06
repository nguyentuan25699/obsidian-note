## 1. What is binary code?
- The computers store and represent data in binaries. Binary is simply a set or a collection of 1s and 0s.
- Each number in a binary, each 1 and 0 in a set are called a Bit, which is a short form of Binary digIT.

Ex: 12 => 1100

- We also have strings, images, and even videos. Computers know how to represent all types of data in binaries.
ex: How will a computer represent the string “L” in binaries? 
To store any character in binaries, Computers will first convert that character to a number, then convert that number to its binary representation.
![[Pasted image 20260705143826.png]]

## 2. Introduction to Buffers
- Data buffer (or just buffer) is a region of physical memory storage used to temporarily store data while it is being moved from one place to another.
- Buffers have a defined and limited size. The size of the buffer is determined by a case-by-case algorithm. Buffering is a technique that was developed to prevent data congestion when traveling from one place to another.

## 3. Buffers in Node.js
- In Node.js, buffers are a special type of object that can store raw binary data. A buffer represents a chunk of memory - typically RAM - allocated in the computer.
- The Buffer class was introduced as part of the Node.js API to make it possible to manipulate or interact with streams of binary data.
![[Pasted image 20260705144446.png]]

## 4. Working with Node.js Buffers
- Create an empty buffer of size 10. // A buffer that only can accommodate 10bytes.
```js
const buf1 = Buffer.alloc(10);
```

- Write data to the buffer
```js
buf1.write("Hello Nodejs Buffer"); // The result of buf1 is "Hello Node", because buf1 is only 10 in size.
```

- Create a buffer with content
```js
const buf2 = Buffer.from("Welcome to Buffer"); //By default, the processing encoding will be utf8 when we do not specify the encoding.

const buf3 = Buffer.from("Welcome to Buffer", "ascii"); //Create a bufferfrom the content with the processing encoding ascii
```

- Read the buffer data
```js
console.log(buf2.toString());
```

- Convert it to string using the toString() function with the default encoding `utf8`
```js
console.log(buf2.toString("hex")); 
// Read the content of buf2 with hexencoding --> result: 57656c636f6d6520746f20427566666572
```

- Examine the size of a buffer
```js
console.log(buf1.length); 
// 10

buf2.length 
// 17. Auto-assigned based on the initial content when created.
```


### References
- https://nodejs.org/dist/latest-v8.x/docs/api/buffer.html 
- https://nodejs.dev/learn/nodejs-buffers
- https://www.programminghunk.com/2020/04/nodejs-buffer-module.html
- https://www.freecodecamp.org/news/do-you-want-a-better-understanding-of-buffer-in-node-js-check-this-out-2e29de2968e8/