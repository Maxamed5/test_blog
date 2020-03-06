+++
title = "Node.js - Event Emitter"
date = "2020-03-06"
draft = false
pinned = false
image = "img/node.js-event-emitter.jpg"
description = "1: Node.js - Event Emitter\n#EventEmitter Class  #on and emit. on\n2: Methods Method & Description  #addListener(event, listener) #on(event, listener) #once(event, listener)\n#removeListener(event, listener)  #removeAllListeners([event]) #setMaxListeners(n)  #listeners(event) #emit(event, [arg1], [arg2], [...])\n3: Class Methods Method & Description #listenerCount(emitter, event)  #Events & Description #\t\nnewListener  #removeListener   #Examples"
+++
<!--StartFragment-->

Many objects in a Node emit events, for example, a net.Server emits an event each time a peer connects to it, an fs.readStream emits an event when the file is opened. All objects which emit events are the instances of events.EventEmitter.

## EventEmitter Class

As we have seen in the previous section, EventEmitter class lies in the events module. It is accessible via the following code −

```

```

When an EventEmitter instance faces any error, it emits an 'error' event. When a new listener is added, 'newListener' event is fired and when a listener is removed, 'removeListener' event is fired.

EventEmitter provides multiple properties like**on**and**emit**.**on**property is used to bind a function with the event and**emit**is used to fire an event.

## Methods

| Sr.No. | Method & Description |
| ------ | -------------------- |
| 1      |                      |
| 2      |                      |
| 3      |                      |
| 4      |                      |
| 5      |                      |
| 6      |                      |
| 7      |                      |
| 8      |                      |

## Class Methods

| Sr.No. | Method & Description |
| ------ | -------------------- |
| 1      |                      |

## Events

| Sr.No. | Events & Description |
| ------ | -------------------- |
| 1      |                      |
| 2      |                      |

## Example

Create a js file named main.js with the following Node.js code −

[Live Demo](http://tpcg.io/4qSKcR)

```
// Import events module
var events = require('events');

// Create an eventEmitter object
var eventEmitter = new events.EventEmitter();
```

Now run the main.js to see the result −

```
Live Demo
var events = require('events');
var eventEmitter = new events.EventEmitter();

// listener #1
var listner1 = function listner1() {
   console.log('listner1 executed.');
}

// listener #2
var listner2 = function listner2() {
   console.log('listner2 executed.');
}

// Bind the connection event with the listner1 function
eventEmitter.addListener('connection', listner1);

// Bind the connection event with the listner2 function
eventEmitter.on('connection', listner2);

var eventListeners = require('events').EventEmitter.listenerCount
   (eventEmitter,'connection');
console.log(eventListeners + " Listner(s) listening to connection event");

// Fire the connection event 
eventEmitter.emit('connection');

// Remove the binding of listner1 function
eventEmitter.removeListener('connection', listner1);
console.log("Listner1 will not listen now.");

// Fire the connection event 
eventEmitter.emit('connection');

eventListeners = require('events').EventEmitter.listenerCount(eventEmitter,'connection');
console.log(eventListeners + " Listner(s) listening to connection event");

console.log("Program Ended.");
```

Verify the Output.

```
2 Listner(s) listening to connection event
listner1 executed.
listner2 executed.
Listner1 will not listen now.
listner2 executed.
1 Listner(s) listening to connection event
Program Ended.
```

<!--EndFragment-->