Virtual Private Networks are for secure communication between networks, or between a client and a network.

VPNs achieve security in a variety of ways.  Often they involve [[Tunneling]]: wrapping packets into the payload of other packets.  There are two main use cases: one is to support protocols that the network doesn't support.  For example, if two LANs use IPv6 internally, and wish to communicate with one another over a network that only supports IPv4, the two endpoints can establish a tunnel.  The IPv6 packets (including headers) can be wrapped in the payload of packets with IPv4 headers.  When the packets reach their destination network, they can be unwrapped and routerd appropriately.

The second major tunneling use-case is encryption.  If headers are encrypted, middle boxes can't route them correctly.  To avoid this, encrypted packets can be wrapped in unencrypted packets and sent to a proxy that can handle the decryption.

VPNs commonly secure communication with either [[IPsec]] protocols (Network layer in [[OSI Model]]) or TLS (LAYER 6 OR 7)