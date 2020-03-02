+++
title = "Node.js "
date = "2020-03-02"
draft = false
pinned = false
image = "img/d0e0afc314344d12b2f0799151939294.png"
description = "1: What is Node.js?\n1: Features of Node.js #Asynchronous and Event Drive #Very Fast #Single Threaded but Highly Scalable #No Buffering #License \n2: Who Uses Node.js? #Concepts  \n3: Where to Use Node.js?\n\n2: Node.js - First Application #Import required modules #Create server #Read request and return response   \n3: Creating Node.js Application #require 3: - Create Server\n#http.createServer()  #listen\n\n"
footnotes = "What is Node.js?\nNode.js is a server-side platform built on Google Chrome's JavaScript Engine (V8 Engine). Node.js was developed by Ryan Dahl in 2009 and its latest version is v0.10.36. The definition of Node.js as supplied by its official documentation is as follows −\n\nNode.js is a platform built on Chrome's JavaScript runtime for easily building fast and scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.\n\nNode.js is an open source, cross-platform runtime environment for developing server-side and networking applications. Node.js applications are written in JavaScript, and can be run within the Node.js runtime on OS X, Microsoft Windows, and Linux.\n\nNode.js also provides a rich library of various JavaScript modules which simplifies the development of web applications using Node.js to a great extent.\n\nNode.js = Runtime Environment + JavaScript Library\n\nFeatures of Node.js\nFollowing are some of the important features that make Node.js the first choice of software architects.\n\nAsynchronous and Event Driven − All APIs of Node.js library are asynchronous, that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data. The server moves to the next API after calling it and a notification mechanism of Events of Node.js helps the server to get a response from the previous API call.\n\nVery Fast − Being built on Google Chrome's V8 JavaScript Engine, Node.js library is very fast in code execution.\n\nSingle Threaded but Highly Scalable − Node.js uses a single threaded model with event looping. Event mechanism helps the server to respond in a non-blocking way and makes the server highly scalable as opposed to traditional servers which create limited threads to handle requests. Node.js uses a single threaded program and the same program can provide service to a much larger number of requests than traditional servers like Apache HTTP Server.\n\nNo Buffering − Node.js applications never buffer any data. These applications simply output the data in chunks.\n\nLicense − Node.js is released under the MIT license."
+++
```
var http = require("http");

http.createServer(function (request, response) {
   // Send the HTTP header 
   // HTTP Status: 200 : OK
   // Content Type: text/plain
   response.writeHead(200, {'Content-Type': 'text/plain'});
   
   // Send the response body as "Hello World"
   response.end('Hello World\n');
}).listen(8081);

// Console will print the message
console.log('Server running at http://127.0.0.1:8081/');
```

![](img/nodejs_concepts.jpg)

![]()
