## Address Resolution Protocol (ARP)
This is the point at which communication transitions from the network layer (usually an IP protocol) to the data link layer in the OSI 7-layer model.

To communicate over data link protocols, the sender must know the physical address (MAC address) of the recipient. ARP is the process by which a network address is mapped to the needed physical address.

An ARP packet essentially contains 4 fields: 
1. Sender protocol (IP) address
2. Sender hardware (MAC) address
3. Receiver protocol (IP) address
4. Receiver hardware (MAC) address

When a host needs to send a packet destined for a certain IP address, it first checks its own cache to see if it already has a MAC address associated with the destination IP. If it does not, it broadcasts and ARP message to all connected hosts. Any host prepared to process packets for the destination IP can respond with its own ARP (does not to be broadcast b/c initial broadcast includes the sender's hardware address).

ARP is also used for [several other purposes](https://en.wikipedia.org/wiki/Address_Resolution_Protocol), e.g. IP address sanity-checking when a new host wants to take ownership of an IP address or addresses.
## Routing tables
On Linux, there are an arbitrary number of routing tables. The OS will try to match packets using each available table in order, from highest-priority table to lowest. View table matching rules with `ip rule show`. Default table priority is:
1. `local`: highest priority table, specific to local machine
2. `main`: the 'normal' table, contains rules for most packets
3. `default`: empty by default, specifies post-processing rules for addresses that did not match on previous tables
Admins can add tables and apply them to certain packets with custom policies.

Routing table `destination` is used to match outbound packets to the appropriate gateway or listener. 

Within a table, matching rules get applied from most to least-specific. The least specific possible route is `destination` 0.0.0.0 with mask 0.0.0.0. That specifies a fallthrough case. The most-specific would be an address with mask 255.255.255.255.

## IP 0.0.0.0
This is a special 'IP address' that has different meanings in different context.

### Listening
When a listening process is bound to address `0.0.0.0` on the host, it means the process should accept incoming from packets from _any_ networking interface on the host. Any arriving packet, whether internal or external, will get routed to the listener provided the ports match.

### As routing table destination
When `0.0.0.0` is specified in the `destination` column of a routing table, it functions as a default, since it's the least-specific possible destination IP.

### As routing table gateway
Gateway value 0.0.0.0 means "there's no gateway for this destination, the current device is directly connected to the correct subnet and no intermediate routing is needed". When this is the case the machine can ARP for the destination MAC address and send the packet directly.