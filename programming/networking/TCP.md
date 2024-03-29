A TCP segment includes the following structure.  Note that *both sides* of the conversation are tracking both *sequence* and *ack* numbers, since both hosts are sending as well as receiving:
1. first 32 bits (bit 0 - 31): source port and destination port
2. bits 32 - 63: Sequence number.  This is the sum of all the bytes the host has sent in previous communication.  If a host has sent 500 bytes, and is now sending 100 more, the sequence number of the current packet will be 500, and the next packet will be 600.  In other words, the first packet the client sends will have a **relative** sequence number 0.  The **actual** sequence number is a randomly-selected 32-bit integer.
3. bits 64 - 95: Acknowledgment number.  Sum of every byte the host has received as part of the current transaction.

The sequence number and acknowledgment number, together with the ACK flag, allow the host and client to check the integrity of the information received and resend packets that may be lost in transmission (in this case, seq/ack numbers will be out-of-sync).  Transmission of every segment is a 2-way exchanges: sender sends the packet, and the receiver sends an `ack` message with its acknowledgement number updated.

TCP connections are stateful, and can have a number of [different statuses](https://www.ibm.com/docs/en/zos-basic-skills?topic=layer-transmission-control-protocol-tcp).  These statuses can be used for fine-grained firewall control through [[iptables]].

Summary:
- TCP connections are stream-oriented: the protocol itself guarantees that data will be handed off in the order it was sent, and there are loss-prevention and error-correction mechanisms