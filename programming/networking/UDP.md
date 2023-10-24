User Datagram Protocol is basically a stripped-down version of [[TCP]].  A UDP header contains a port number and a destination IP address, nothing more.  There is no acknowledgment from the receiver, and their is no stateful connection.  Because of this, UDP packets are smaller than TCP, and there is less packet exchange in total because there is no `ack`.  Under good network conditions, this makes UDP more performant., but because there is no recovery from lost/corrupted packets, the receiver is hosed if network conditions are bad.

[[WebRTC]] and other real-time protocols are based on UDP for performance reasons.

Summary:
- UDP is connection-less, and does not offer guarantees about flow-control, deduplication, order, or completeness offered by [[TCP]]. 
- In exchange for fewer guarantees, UDP is much more performant.