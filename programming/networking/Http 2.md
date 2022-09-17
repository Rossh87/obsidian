Http 2 offers several improvements that address shortcoming in [[Http 1.1]].  These include:
- [[Http multiplexing]]
- Enables compression of Http headers as well as bodies
- [[Server push]] (something of a dud, it seems)

The major shortcoming of Http 2 is that there can still be head-of-line blocking in the [[TCP]] layer.  This happens because TCP is essentially a 'single-threaded' process: there is one, continuous flow of packets from sender to receiver, and if a single packet is lost, the flow stops until the packet can be re-transmitted.  When this happens, the [benefits of multiplexing are entirely negated](https://http3-explained.haxx.se/en/why-quic/why-tcphol).  In fact, on connections with high rates of packet loss, the user might be better of with Http 1, since having multiple TCP connections open provides more streams over which the loss can be distributed, resulting in less blocking time overall.

Addressing this problem is the major driver behing [[Http 3]] and [[QUIC]].