# Websockets

## Use
Enable real-time communication between client and server.  A limitation of HTTP is that is is strictly one-directional: the client must initiate an interaction by sending a request.  Applications that require the client to receive events from the server whose timing cannot be known in advance have in the past solved this problem through long-polling: the client sends a request with a long timeout, and the server can respond whenever it has data.  However, this approach ties up some server resources for the duration of the waiting request, even while the server has no data to send.  The websocket protocol addresses this inefficiency.

Because websocket connections only require headers to be sent for the handshake, data exchange can be several times faster than HTTP.

## Implementation
The websocket protocol is initiated by an HTTP request, and uses an [[TCP]] connection, but is its own protocol (not HTTP). The initial HTTP request is a "handshake": the client indicates in the request headers that it would like to initiate a websocket connection with the server.  If the server is willing and able to comply, the connection is set up over the TCP connection that the initial HTTP request was sent on.

A websocket URI uses a custom scheme `ws`, or `wss` for secure connections, instead of `http(s)`. The request to initiate the WS connection sets the following headers:
- `Connection: Upgrade`: signals connection should be kept alive, and will be used for non-HTTP requests
- `Upgrade: websocket`: specifies the specific protocol requested to supercede HTTP
- `Sec-Websocket-Key: [base64 encoded nonce]`
- `Sec-Websocket-Version: 13`: 13 is the **only** acceptable protocol version.

If the server agrees to the WS connection, it responds with an HTTP `101: switching protocols response`.  Response includes the first two headers above, and `Sec-Websocket-Accept`, which contains a SHA-1 hash of the client's `Websocket-Key` (above) and a constant value.  The purpose of exchanging these hashes is for each participant to prove they support Websockets appropriately.  Websocket payloads are obfuscated with a bitmask to prevent caches and proxies from incorrectly caching WebSocket frames as if they were HTTP frames.  If this does occur, it is a [[cache poisoning]] vulnerability.

Either client or server can close the connection by sending a frame with the 'close' `opcode`. If either party receives a close frame, it must respond with its own close frame, and no more data should be sent.  The TCP connection is then torn down.

C.f.
[This article](https://sookocheff.com/post/networking/how-do-websockets-work/) for most of the above info
[rfc6545](https://www.rfc-editor.org/rfc/rfc6455)
