Very similar to [[Unix sockets]], with some key differences

Steps:
1. A process (the server) makes a `syscall` to `socket()`, specifying the address family (IP4/IP6) and the protocol (tcp/udp). A uniquely-identifying integer for the resulting socket is returned.
2. The server binds to an IP address and port. This becomes the 'endpoint' for the process.
3. (TCP only) The server socket goes into a 'listening' state. Clients can then `connect` using the IP address/port 'endpoint'. Requests to connect to the listening socket go into a queue, and the server can choose to accept or reject connection requests. If a connection request is accepted, an new socket associated with the client socket is created, and communication can begin on that socket pair. Importantly, the original listening socket does NOT handle communication.
4. Either party can close their socket. After closing, the socket cannot send further information. Unlike Unix sockets, closing a network socket automatically releases associated resources.

Both [[TCP]] and [[UDP]] communications can re-use the same socket (port multiplexing).  For TCP, this means the same socket is re-used for multiple connections. For connection-less UDP, it simply means that individual packets can arrive on the same socket from multiple sources.