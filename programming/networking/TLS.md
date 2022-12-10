Sometimes called SSL, but this term is technically obsolete.

General structure is that client and server use public/private key pairs (e.g. RSA) to asymmetrically encrypt and share a session key, which is then used to *symmetrically* encrypt further exchanges.  This is necessary because symmetric encryption is computationally much cheaper than asymmetric.

The information critical in establishing a TLS connection is contained in an x509 certificate, issued by one of many *certificate authorities*.  In addition to containing the server's public key, the certificate is signed by the CA, allowing the client to verify that the server it is communicating with is actually administered by the owner of the domain to which the cert was issued.  

TLS 1.3 optimizes several aspects of TLS 1.2.  Most notably, the TLS handshake (certificate exchange) in TLS 1.2 takes 2 round-trips, while 1.3 only takes one.  In addition, TLS 1.3 does not use public/private key exchange to establish the session key.  Instead, an algorithm like Diffie-Helman is used to establish a shared session key without ever transmitting the key from client to server.