---
date: 2026-07-05
tags:
  - code
  - learning
  - js
draft: false
---
## 1. What are callbacks?
- A callback is a function which is called when a task is completed, thus helps in preventing any kind of blocking and a callback function allows other code to run in the meantime
- Using Callback concept, Node.js can process a large number of requests without waiting for any function to return the result which makes Node.js highly scalable

## 2. The problems with callbacks
- Callback hell: https://callbackhell.com/
- Difficult to reason about
- Error handling is difficult
- Problem with "this"

Callback hell solving
- Keep code clean
- Modularize
- Handle every single error
- ES6: Promise, async/await


### Promise
- Allows you to associate handlers with an asynchronous action's eventual success value or failure reason. This lets asynchronous method return values like synchronous methods: instead of immediately returning  the final value, the asynchronous method returns a promise to supply the value at some point in the future.
- A promise os one of these states: 
	- pending: initial state, neither fulfilled nor rejected
	- fulfilled: meaning that the operation was completed successfully
	- rejected: meaning  that the operation failed

**![[Pasted image 20260703102511.png]]**

