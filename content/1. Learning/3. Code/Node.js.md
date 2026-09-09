---
date: 2026-07-01
tags:
  - code
  - learning
draft: true
---
## I. Bức tranh tổng thể
### 1. [[JavaScript]] vs NodeJS vs [[Express]]
- **[[JavaScript]]** là ngôn ngữ
- **NodeJS** là môi trường chạy [[JavaScript]] ở ngoài trình duyệt
- **[[Express]]** là framework chạy trên NodeJS để viết backend/[[API]] dễ hơn
```text
Từ ấy trong tôi bừng nắng hạ
```





-----------------------------------------
## 1. Node.js REPL
- REPL also known as Read-Evaluate-Print-Loop is a programing language environment (basically a console window) that takes single expression as user input and return the result back to the console after execution.
- How to use: Type `node` command on terminal

```js
>$ node
>$ console.log('Hello Node.js");
>
> Hello Node.js
> undefined
```

## 2. [[npm]]
- Node package manager

## 3. Event loop
The [[Event loop]] is what allows Node.js perform non-blocking I/O operations, despite the fact the javascript is single-threaded - by offloading operations to the system kernel whenever possible.

## 4. Callbacks
- A [[Callback in Node.js]] is a function which is called when a task is completed, thus helps in preventing any kind of blocking and a callback function allows other code to run in the meantime
- Using [[Callback]] concept, Node.js can process a large number of requests without waiting for any function to return the result which makes Node.js highly scalable

## 5. Event emitter
- Introduction the [[Event emitter]]
- EventEmitter class
- Methods & Events

## 6. Modules
- [[Modules]] introduction
- Node.js module Types
- Export Module in Node.js

## 7. [[Web module]]
- Introduction HTTP Module
- Working with HTTP Module
- Introduction URL Module
- Working with URL Module

## 8. [[Buffers]]
- What is binary code?
- Introduction to Buffers
- Buffers in Node.js
- Working with Buffers Node.js

## 9. [[Streams]]
- What are Streams? 
- Why use Streams? 
- Streams in Node.js 
- Working with Node.js Streams

## 10. [[Express - Nest]]
