## 1. Introduction

The Event loop is what allows Node.js perform non-blocking I/O operations, despite the fact the javascript is single-threaded - by offloading operations to the system kernel whenever possible.

- Handling user request in Node
![[Pasted image 20260702095835.png]]

- The event loop simply iterate over the event queue (list of events and callbacks)
- Node start event loop by checking for nay expired timers in the timers queue, go through each queue in each step while maintaining a reference counter of total items to be processed
- After processing the close handlers queue, if there are no items to be processed in any queue, the loop will exit

## 2. Event Loop's phase
- Timers: callbacks scheduled by  *setTimeOut()*  or *setInterval()* are executed
- pending callbacks: execute I/O callbacks deferred to the next loop iteration
- ide, prepare: only used internally
- poll: retrieve new I/O events, execute I/O related callbacks (almost all, exception of close callbacks, scheduled by timers, *setImmediate()*)
- check: *setImmediate()* callbacks are invoked here
- close callbacks: some close callbacks, .e.g.  socket.on('close', ...)
![[Pasted image 20260702100928.png]]

## 3. The call stack
- The call stack is LIFO (last in, first out) stack
- The event loop continuously tha call stack to see if there any function that needs to run. While doing so, it adds any function call it find to the call stack and execute each one in order

## 4. The simple Event Loop
- When *`setTimeout()`* is called, the browser or Node.js starts the timer. Once the thmer expires, in this case immediately as we put 0 as the timeout, the callback function is put in the Message Queue.
	- "The loop gives priority to the call stack, and it first provesses everything it finds in the call stack, and once there's nothing  in there, it goes to pick up thing in the message queue"