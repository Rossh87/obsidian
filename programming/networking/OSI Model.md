https://www.cloudflare.com/learning/ddos/glossary/open-systems-interconnection-model-osi/

Open Systems Interconnection model breaks internet communication down by layers of responsibility.  Each layer interacts with other layers.

Useful acronym: Please Do Not Throw Sausage Pizza Away

1. **Physical Layer** is the physical material that conducts signal, and responsible for converting data into a bit stream.  Includes things like cables and switches.
2. **Data Link Layer** facilitates data transfer betwen devices on the *same* network. Breaks packets from the network layer into smaller pieces called frames.  The major protocol at this level is the *ethernet* protocol.  IP *packets* built by the network layer are wrapped in **frames** that follow the ethernet protocol.  Most notably, these frames include **Media Access Control** addresses of the sender's and receiver's network interfaces.
3. **Network Layer** facilitates data transfer between *different* networks. Major protocol for this layer is the **internet protocol (IP)**.  Responsible for wrapping transport layer segments into packets.  Also responsible for routing packets on the best physical path to destination.
4. **Transport Layer** handles end-to-end communication between devices.  [[TCP]] is an example of a transport layer protocol.  Transport layer breaks data into chunks, called segments, and hands them off to network layer.  These chunks include source port, host port, and other protocol-specific information. The other party's transport layer is responsible for reassembly.  Transport layer is also responsible for flow control (sending/receiving at a rate that doesn't overwhelm either party), and error handling (noticing and re-transmitting failed data).
5. **Session Layer** opens and closes communication between two devices.  The session is the time from conn open to conn close. Session prevents connections from remaining open too long.  Session also tracks the status of transfers with checkpoints.  If a transfer fails, the session can be resumed from the last checkpoint.
6. **Presentation Layer** is a formatter.  Data encryption, compression, and encoding all get handled here.  Responsible for presenting data to application layer that app layer can consume.
7. **Application Layer** directly interacts with data from user.  NB it is **not** the client software application itself; rather, it is the protocols and data manipulation the client software relies on.  HTTP and SMTP (mail transport protocol) are both application layer protocols.

The OSI model is a conceptual framework that is protocol independent.