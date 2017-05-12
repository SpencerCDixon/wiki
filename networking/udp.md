# User Datagram Protocol (aka unreliable data protocol)

**Why does it exist?**
* primary feature --> it lacks lots of features of TCP
* WebRTC is built on top of UDP making it more relevant in today's world  
  + this makes sense b/c it's okay for a voice/video packet to not be delivered

UDP adds a few headers on top of IP:

* Source port
* Destination port
* Length
* Checksum


