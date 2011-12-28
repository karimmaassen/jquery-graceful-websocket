# The Graceful WebSocket

So, you want to start building realtime event driven applications using the new HTML5 WebSocket API?

 - You want it to work in all browsers, no matter if they have WebSocket support or not
 - You don't want to rely on proprietary technology such as Flash to provide a fallback
 - And naturally, you don't want to write more than one implementation

**Introducing, the gracefulWebSocket jQuery plugin:**

 - Implements the w3c WebSocket interface
 - Wraps the native WebSocket if support is detected
 - Provides a default fallback using traditional AJAX polling over HTTP
 - Requires no extra code on the frontend, allows you to target the WebSocket API today and let users take advantage of it as more browsers add support.
 - Default fallback behavior can be overridden by plugin options

Contact: http://twitter.com/ffdead

## Basic Usage

Basic usage is very straight forward. The whole purpose of this plugin is to enable developers to use the WebSocket API to write applications, even if the browser doesn't support it.

Include plugin

```html
// include the plugin
<script type="text/javascript" src="jquery.gracefulWebSocket.js"></script>
```

Open WebSocket

```js
// open socket using standard syntax
var ws = $.gracefulWebSocket("ws://127.0.0.1:8080/");
```

Sending

```js
// send message to server using standard syntax
ws.send("message to server");
```

Receiving

```js
// listen for messages from server using standard syntax
ws.onmessage = function (event) {
   var messageFromServer = event.data;   
};
```

## Graceful degradation explained

The gracefulWebSocket will automatically revert to fallback mode if no native WebSocket implementation can be detected in the browser.

A fallback object implementing the same interface with be returned instead, which uses HTTP POST to send messages to the server, and polling HTTP GET requests to retrieve new messages from the server.

```js
// in fallback mode: connect returns a dummy object implementing the WebSocket interface
var ws = $.gracefulWebSocket("ws://127.0.0.1:8080/"); // the ws-protocol will automatically be changed to http
// in fallback mode: sends message to server using HTTP POST
ws.send("same message to server, this time send using a POST request");
// in fallback mode: listens for messages by polling the server using HTTP GET
ws.onmessage = function (event) {
   var sameMessageFromServer = event.data;   
};
```

## More info

http://www.slideshare.net/ffdead/the-html5-websocket-api

## MIT License

Copyright (c) 2010 David Lindkvist
