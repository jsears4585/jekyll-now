## Two-way Communication

### What are they?

```
The WebSocket Protocol enables two-way communication between a client
running untrusted code in a controlled environment to a remote host
that has opted-in to communications from that code.  The security
model used for this is the origin-based security model commonly used
by web browsers.  The protocol consists of an opening handshake
followed by basic message framing, layered over TCP.  The goal of
this technology is to provide a mechanism for browser-based
applications that need two-way communication with servers that does
not rely on opening multiple HTTP connections (e.g., using
XMLHttpRequest or <iframe>s and long polling).
```

![WS Meme 2](http://cdn.jsears.co/ws-meme-2.jpg "WS Meme 2")

### How it works

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

![WS Client Adoption Chart](http://cdn.jsears.co/websocket-adoption-chart.png "WS Client Adoption Chart")

### End

![WS Meme](http://cdn.jsears.co/ws-meme.jpg "WS Meme")
