---
date: 2026-07-05
tags:
  - code
  - js
  - learning
draft: false
---
## 1. Introduction the Event emitter
- If you worded with JavaScript in the browser, you know how much of the interaction of the user is handled through events: mouse clicks, keyboard button presses, reacting to mouse movements, and so on.
- On the backed side, Node.js offers us the option to build a similar system using the events module.
![[Pasted image 20260703103335.png]]

## 2. EventEmitter class
- This module, in particular, offers the EventEmitter class, which we'll use to handle our events
- You initialize that using
```js
const EventEmitter = reuquire('event');
const eventEmitter = new EventEmitter();
```

- This object exposes, among many others, the **on** and **emit** methods.
	- **emit** is used to trigger an event
	- **on** is used to add a callback function that's going to be executed when the event is triggered
```js
eventEmitter.on('start', () => {
	console.log('started');
});

eventEmitter.emit('start');
```

 - You can pas arguments to the event handler by passing them as additional arguments to **emit()**: 
```js
evnetEmitter.on('start', nummer => {
	console.log(`started ${number}`)
})

eventEmitter.emit('start', 23)
```

- Mutliple arguments:
```js
eventEmitter.on('start', (start, end) => {
	console.log(`started from ${start} to ${end}`)
})

eventEmitter.emit('start', 1, 100)
```

## 3. Methods & Events
- The EventEmitter object also exposes several other methods to interact with events, like
	- **once()**: add a one-time listener removeListener()
	- **off()**: remove an event listener from a event
	- **removeAllListeners()**: remove all listeners for an event

More detail:
- https://nodejs.org/api/events.html
- https://nodejs.dev/learn/the-nodejs-event-emitter

