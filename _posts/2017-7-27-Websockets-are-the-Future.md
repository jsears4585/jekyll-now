## Two-way Communication

### A little history

```
Historically, creating web applications that need 
bidirectional communication between a client and a server 
(e.g., instant messaging and gaming applications) has required 
an abuse of HTTP to poll the server for updates while sending 
upstream notifications as distinct HTTP calls [RFC6202].

This results in a variety of problems:

   o  The server is forced to use a number of different 
      underlying TCP connections for each client: one 
      for sending information to the client and a new 
      one for each incoming message.

   o  The wire protocol has a high overhead, with each 
      client-to-server message having an HTTP header.

   o  The client-side script is forced to maintain 
      a mapping from the outgoing connections to the 
      incoming connection to track replies.

A simpler solution would be to use a single TCP connection 
for traffic in both directions.  This is what the WebSocket 
Protocol provides.  Combined with the WebSocket API [WSAPI], 
it provides an alternative to HTTP polling for two-way 
communication from a web page to a remote server.
```

![Carlton Fail](http://cdn.jsears.co/carlton.gif "Carlton")

Hmm, sounds good, but I think we can unpack this a little more...

Communication over the internet generally happens in a stateless, ***request-response*** manner. When you request a website's information online, you and the server agree (or don't) via a series of handshakes, and then the server (if you've been successfully authorized) sends you the resources you requested with a response of it's own. Each handshake and series of responses and requests is distinct from the other.

As usual, HTTP doesn't allow the server to send you resources without you specifically requesting them.

The WebSocket protocol, once allowed, acts as an ***upgraded***, persistent TCP connection that allows the client and the server to engage in two-way communication and provides an alternative to repeated polling cycles and their accompanying overhead. WebSocket channels aren't just bi-directional (or full-duplex), they're also persisted until either party closes the connection manually or the channel is disconnect.

Also, and this point shouldn't be neglected either, the WebSocket protocol allows you to manage connections from multiple clients and then actively push them information.

Now that's cool.

![WS Meme 2](http://cdn.jsears.co/ws-meme-2.jpg "WS Meme 2")

### Upgrading connections

Straight from the RFC:

```
The WebSocket Protocol is an independent TCP-based protocol.  Its
only relationship to HTTP is that its handshake is interpreted by
HTTP servers as an Upgrade request.

By default, the WebSocket Protocol uses port 80 for regular WebSocket
connections and port 443 for WebSocket connections tunneled over
Transport Layer Security (TLS) [RFC2818].
```

The WebSocket Protocol is initiated with a handshake from the client, requesting to engage in an upgraded connection with the server. 

![WS Handshake](http://cdn.jsears.co/ws-example-handshake-client.png "WS Handshake")

Once the server agrees, the WebSocket Protocol becomes enabled and both client and server are allowed to issue communication to each other at will without requiring AJAX or long polling. 

![WS Protocol Chart](http://cdn.jsears.co/protocol-chart.png "WS Protocol Chart")

### Adoption in modern browsers

Although it used to be more of a concern (also security), websockets are now generally very well implemented across client browsers, including mobile.

[Check to see if your browser supports websockets here](http://websocketstest.com/)

![WS Client Adoption Chart](http://cdn.jsears.co/websocket-adoption-chart.png "WS Client Adoption Chart")

### Use Cases

So you might be asking yourself, when might WebSocket protocol benefit me in the future as a developer? What kind of applications might make the most out of websockets?

Exactly two sitiations: chatrooms and gaming. ***Drops mic, leaves stage***

Seriously though, the opportunities are endless. Next time you see a need for open communications between your application and the client, or need to push information to all connected clients simultaneously, consider trying out a WebSocket protocol implementation.

Some other options:

- Live teaching
- Co-drawing or co-writing
- Email clients
- Any other multi-user, realtime applications

![WS Meme](http://cdn.jsears.co/ws-meme.jpg "WS Meme")
