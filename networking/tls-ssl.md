# TLS - Transport Layer Security

### History

* SSL was originally developed at Netscape to allow for ecommerce transactions.
* Since SSL was proprietery to Netscape it was then formed into TLS by IETF.
* TLS has gone through a few versions due to known security breaches.  Therefore, it's best to use the latest version always


TLS has there main purposes:

1. Encryption
2. Authentication
3. Integrity

Before anything can really begin the connected peers must agree on which
ciphersuites will be used and the keys used to encrypt/decrypt the data.


This works due to [asymmetric key cryptography](https://www.youtube.com/watch?v=EPXilYOa71c).  This process allows the clients to share
a secret over an insecure connection which then enables all subsequent exchanges
to be secure.  People listening to the traffic may be able to determine the
endpoints and how much data is being sent back and forth but they'll never be
able to determine _what_ data is being sent across the wire.

Another aspect of this exchange is being able to authenticate identities.  That
way you know when you're communicating with your bank you're **actually**
communicating with your bank and someone is not spoofing it's name/IP address.

**Important Perf**: all TLS connections will require up to two extra roundtrips
on top of the TCP handshake to negotiate the cryptography.  This has serious
performance implications and it's important to be aware of.

**Problem**: What if we have a server that wants to host multiple websites, each
with it's own TLS certificate, on the same IP address?

**Solution**: SNI Server Name Indication

SNI is like a NAT for your server to select the correct certificate.  It is a
map that will check the hostname and then pick the appropriate cert to use in
the TLS handshake.

---
One way to mitigate the perf problems of TLS connections is to use a session
cache.  When the negotiation is successful the client and server both save a
unique session ID locally.  Then when the client re-connects in the future it
can pass along that session ID and if the server recognizes it, it can skip a
roundtrip step.

This can get difficult to manage if you have clients opening up many connections
in parallel to fetch resources faster and/or many server deployments.  It's
worth looking into if you have high traffic concerns or a relatively straight
forward deployment.

### Chain of Trust
Boils down to:  

* I share keys with my friend Coleman
* I then meet Aidan who is friends with Coleman
* Aidan uses Colemans key to prove to me he really is friends with Aidan
* I can then trust Aidan.

The whole internet is built upon this chain of trust and there are a few ways it
can start.

1.  You can manually specify on your computer which certificates you trust  
2.  You can follow the chain coming form a CA (Certificate Authority)  
3.  Most OS's/browsers have pre-filled certs that they will trust  
