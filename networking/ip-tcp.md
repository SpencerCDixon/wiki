# IP/TCP 

**IP** - (Internet Protocol) provides host-to-host routing and addressing.
**TCP** - (Transmission Control Protocol) is what provides a reliable network
running over an unreliable channel.

TCP/IP are often known together as the "Internet Protocol Suite" and were first
proposed by Vint Cert/Bob Kahn in 1974.

## Connecting

All TCP connections begin with a three-way handshake before any data can be
transferred.  It kind of reminds me of OAuth.

1. SYN - client picks random sequence number X and sends a SYN packet which can
   also include other TCP flags/options.

2. SYN ACK - Server increments X by one, picks own random sequence Y, adds it's
   own flags, and dispatches response.

3. ACK - client increments both X and Y by one, completes handshake by
   dispatching the last ACK packet.

![Three way handshake](./assets/3-way-handshake.svg)

Client can send a data packet as soon as the ACK packet is dispatched.

**What are the implications of the 3-way handshake?**
Each new connection will have a full roundtrip of latency before any app data
can be transferred!  New TCP connections are expensive and it's pivotal to try
and reuse connections.

**Slow Start** & **Slow Start Restart**  
TCP ramps up congestion window sizes slowly over time.  SS inits the connection
with a conservative window and for every roundtrip doubles the amount of data
that can be sent.  Once a packet is lost the _congestion avoidance_ algorithm
takes over.

**Congestion avoidance** assumes that there is a congested link/router somewhere
that was forced to drop packets.  It will reset the congestion window to
minimize further loss.

**HOL** (Head of line) blocking:
Because TCP traffic must be sent in order, if a packet is lost then all other
packets build up and wait in the buffered queue until the lost packet can be
resent and received by the server.  These delays are commonly referred to as
_jitter_.

