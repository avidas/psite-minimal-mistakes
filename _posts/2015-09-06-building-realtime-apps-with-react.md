---
layout: post
title: "Building Realtime Apps with React, Socket.io and Node.js"
date: 2015-09-06 11:16
comments: true
published: true
categories: Software Javascript React Node.js Socket.io
---

> Update: Udemy has generously granted a free coupon for the readers of this blog for their [React JS and Flux](https://www.udemy.com/learn-and-understand-reactjs/learn/) course. Use the code `avidasreactjs` and the first 50 readers will get free access to the course!

The importance of delivering realtime feedback to users is more than ever. Gone are the days when chats or games were the only applications of realtime software. Starting from finance, advertising or education, having a realtime component to your web application will elevate the user experience.

###Socket.io
From [socket.io's homepage](http://socket.io/), it is a library that enables real-time bidirectional event-based communication. It has two parts, a client side library that runs in the browser and a server side library for node.js. In recent times, this has become the de facto way of doing realtime web applications in the node.js world. Key reasons behind this has been the way it abstracts away the overhead of maintaining multiple protocols, while carrying on similar primitives from [Node streams](https://nodejs.org/api/stream.html) and [eventEmitter](https://nodejs.org/api/events.html). Some of its other powerful features include being able to stream Binary data, broadcast to multiple sockets and being able to manage connected client data from the server.

###Architecture
The WebSocket protocol is a W3C standard that enables interactive communication between browser and server. It functions as an Upgrade request over HTTP 1.1. However, since all legacy browsers and devices do not have support for WebSockets, it's cross-platform abilities get limited.

Socket.io itself is a library to build realtime applications. It will try to upgrade to and use the Websocket protocol if available. Socket.io depends on another libray called Engine.io which exposes a Websocket like API but provides fallbacks to other transport mechanisms such as XHR and JSONP polling. This enables application developers to write realtime codebases that are browser, device and transport implementation independent. 

###Getting started with Socket.io
This tutorial assumes that you have Node.js, npm and Express on your system.

In a directory create two files called index.html and app.js. In your app.js file, add the following

```javascript
var app = require('express')();
var server = require('http').Server(app);
var swig = require('swig');
var path = require('path');

// view engine setup
app.engine('html', swig.renderFile);
app.set('view engine', 'html');

// server and routing
server.listen(8080);
app.get('/', function (req, res) {
  res.render('index');
});
```

We set up the view engine and serve up a basic index page. If this part looks unfamiliar, please check out [Express docs](http://expressjs.com/guide/routing.html). Now add the following in app.js.

```javascript
var io = require('socket.io')(server);
// socket.io demo
io.on('connection', function (socket) {
  socket.emit('server event', { foo: 'bar' });
  socket.on('client event', function (data) {
    console.log(data);
  });
});
```
 We create a new instance of socket.io and pass in the created express server as a parameter. As the server listens, whenever a new client starts a connection, we emit an event called server event and send the payload { foo : 'bar' }. It also listens for 'client event' and logs the payload once it gets the event.

In your index.html file add the following 
```html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
  socket.on('server event', function (data) {
    console.log(data);
    socket.emit('client event', { socket: 'io' });
  });
</script>
```
It includes the client side socket io library. After instantiating a new connection, it listens for the 'server event' and when that event happens it logs the data and emits 'client event' and sends the payload { socket: 'io'}. 

Run node app.js and fire up localhost:8080 in your browser. On the terminal you should see { socket: 'io' } and on the console you should see { foo : 'bar' } printed out. Congrats, you just did your first Socket.io app!

###Useful Socket.io Concepts

##### Message sending/receiving
Socket.IO allows you to emit and receive custom events. Besides connect, message and disconnect, you can emit custom events and send with associated payload. Emit and Broadcast are ways to send events and on is the event listener. 

##### Server vs Client API
There are some common functions between server and client side, but it is worth looking into the docs and understanding what is possible on the server vs client. Generally, the server side has much more features and capabilites and is capable of creating rooms and namespaces but both sides and send and respond to events.

##### Rooms and Namespaces
Socket.io provides built in abstractions to demultiplex the connected clients. Namespaces, identified by a path, can be connected via the following

```javascript
var socket = io(); //connects to default namespace "/"
var admin = io("/admin"); //connects to the namespace specified by the path "/path"
```

After a client connects with ```var socket = io('/admin')``` , we can send message only to the admin namespace.

```javascript
admin.emit("admin alert", "website traffic is up!"); //the event will only be sent to the clients who connected to the admin namespace
```

This enables more role or other criteria based distribution of socket.io events/messages within your application.

Rooms provide a way to further divide up clients within individual namespaces. Clients within a namespace can join and leave a room. By default, a client always is connected to a room idenfied by the sockets id. Hence it is possible to send targeted messages to a connected client via ```socket.broadcast.to(<SOCKET.ID>).emit('test', 'message')```. Rooms could make more sense for particular themes whereas namespaces seem to fit well for user type/responsibilities.

###React and Socket.io
Now for the exciting part, integrating React.js and Socket.io into an application. React.js is Javascript UI framework from facebook. You can follow some of the [initial docs](https://facebook.github.io/react/) to get started with React. This tutorial will not go into great detail into the terminologies of React.js but refer to the official documentation if any of the React syntax looks confusing.

The basic idea of the app is to have an html input and a label. When someone types in something into the input box, it will update the label for anyone else who have an window open except for the person typing. 

##### Client side code
Let's start by changing your index.html to the following

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.2/react.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/0.13.2/JSXTransformer.js"></script>
    <script src="/socket.io/socket.io.js"></script>
  </head>
  <body>
    <div id="mount-point"></div>
    <div id="label-mount-point"></div>
    <script type="text/jsx">
     /** @jsx React.DOM */
    var socket = io();

    var Input = React.createClass({
      _notifyServer: function(event){
        socket.emit('client event', { value: event.target.value });
      },
      render: function(){
        return (
          <div className="update-label">
            <input type="text" placeholder="Enter text" onChange={this._notifyServer}/>
          </div>
        );
      }
    });
    var Label = React.createClass({
      _onUpdateLabel: function(data) {
        this.setState(serverValue: data.value);
      },
      getInitialState: function(){
        return { serverValue: '' };
      },
      render: function(){
        return (
          <div class="my-label">
            <h2>{this.state.serverValue}</h2>
          </div>
        )
      }
    });
    var input = React.render(<Input/>, document.getElementById('mount-point'));
    var label = React.render(<Label/>, document.getElementById('label-mount-point'));
    socket.on('update label', function (data) {
      label._onUpdateLabel(data);
    });
    </script>
  </body>
</html>
```

#####Server side
The server side of the codebase can mostly stay the same, except we broadcast 'update label' when 'client event' is received.

```javascript
io.on('connection', function (socket) {
  socket.emit('server event', { foo: 'bar' });
  socket.on('client event', function (data) {
    socket.broadcast.emit('update label', data);
  });
});
```
#####Explanation
On the client side, two React components called Input and Label are created and mounted by calling React.render. Input renders an html input box which calls the _notifyServer method whenever the someone types into the input field. The _notifyServer method then emits socket.io event called 'client event' with the value of the input box. 

On the server side, when 'client event' is received with the data, the server calls socket.broadcast.emit and passes the data payload along. This means that all the connected clients except for the socket that generated 'client event' will receive the 'update label' event and the payload. This sends the message to everyone except for the person typing.

Back to the client side, the Label component consists on a div with a h2 element with is set to the serverValue state of the component. [getInitialState](https://facebook.github.io/react/docs/component-specs.html#getinitialstate) sets the initial value to be '' so initially the Label is empty. When 'update label' is received, we call the _onUpdateLabel on label, which is an instance of Label. It sets the serverValue state of the Label component to data.value. This invokes the render method of the label component, and it generates a h2 header with the updated value of the serverValue.

<!-- more -->

###Advantages of Socket.io

Many advantages of socket.io are

1. The simplicity of the integration. Rolling your own realtime library is considerably more difficult due to multi-protocol, browser and device requirements.
2. Large community of users and support in multiple platforms. It is used from large companies to small startups, meaning developer support is in abundance. Socket.io released native clients on iOS and Android this year, expanding its reach.
3. It is stable as 1.0.0 has been released in 2014
4. It is completely free

###Disadvantages of Socket.io
1. Socket.io has its own protocol, and it would not work with any custom Websocket implementation by default. The team has worked on this and support for this is getting better http://socket.io/docs/#using-it-just-as-a-cross-browser-websocket
2. Scaling across multiple servers when you have too many open connections for a single server is not something that you will get out of the box with socket.io
3. As with Realtime software, debugging can be complicated and you may need to include Redis or other layers of persistance if you want to gurantee message delivery

Realtime on web and mobile is a secret sauce for many websites and apps these days and Socket.io is a dominant technology in that field. There are entire startups which would not be possible without Socket.io and definitely deserves a place in any web/mobile developers skills of expertise.