## Websockets

### What are they?

Straight from the RFC:

```
The WebSocket Protocol is an independent TCP-based protocol.  Its
only relationship to HTTP is that its handshake is interpreted by
HTTP servers as an Upgrade request.

By default, the WebSocket Protocol uses port 80 for regular WebSocket
connections and port 443 for WebSocket connections tunneled over
Transport Layer Security (TLS) [RFC2818].
```

### How it works

An important thing to understand about the WebSocket Protocol is that it's an upgraded connection:

![WS Protocol Chart](http://cdn.jsears.co/protocol-chart.png "WS Protocol Chart")

### Adoption in modern browsers

![WS Client Adoption Chart](http://cdn.jsears.co/websocket-adoption-chart.png "WS Client Adoption Chart")
