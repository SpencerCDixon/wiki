# General Networking Notes

**Latency** - The time from the source sending a packet to the destination
receiving it.

**Bandwidth** - Maximum throughput of a logical or physical communication path.

Can think of bandwidth as the X/Mbps that you're currently getting.  How big is
the pipe you're sending bits through?  Latency can be though of as the response
time from your computer to whatever other server you're communicating with.
What is the time it takes for the packet to travel from origin to destination?

## Latency Broken Down

* Propagation delay - generally close to speed of light, is determined by material packets are being sent in  
* Transmission delay - determined by bandwidth.  What is the size of the link?  1Mbps/100Mbps  
* Processing delay - time for router to examine packet headers and determine outgoing route, etc.  
* Queuing delay - if router buffer fills up packets spent in the queue will build up this type of delay  

Total latency is the culmination of all the above delays.

**Bufferbloat** - a problem that can occur in your local router.  Routers have
been shipping with large buffers in order to ensure no packet loss.  This goes
against TCP's congestion avoidance mechanisms which then creates variable
latency delays in the network.

Propagation: speed of light is 299,792,458 meters per second.  Unfortunately, we
don't send packets in a vacuum.  We use fiber or copper cables which reduce this
"perfect" speed.  The **refractive index** is the adjusted speed that the
packets can travel in various materials.  Larger value == slower light travel.

Fiber is around ~1.5 refractive index giving us speeds of 200,000,000
meters/sec. Which is FUCKING CRAZY when you think about it.

NYC --> SF = 21ms in fiber  
NYC --> London = 28ms in fiber  

"Lag" is perceived at around 300ms.  Anything under 300 is perceived as
essentially instant to the human eye.

**Why CDN's**: this all boils down to why CDN's are so valuable.  If a round
trip request from NYC to Sydney is going to be ~300ms that leaves no room for
application logic.  CDN's allow us to move the servers closer to our clients
therefore giving more leeway for our applications.

Ironically, the "last mile" is often the slowest.  There is generally 18-44ms of
latency to the closest node in your ISP's core network.  It's often faster for
packets to travel across the ocean than it is to get it from your bedroom to its
next point of contact!

Running `traceroute` can give you some insight into your local jumps
```sh
$ traceroute google.com
traceroute to google.com (172.217.7.238), 64 hops max, 52 byte packets 1 10.0.1.
1 (10.0.1.1)  3.015 ms  0.956 ms  0.811 ms 
2  96.120.66.93 (96.120.66.  93)  10.210 ms  9.596 ms  10.930 ms 
3  68.86.231.21 (68.86.231.21)  10.608 ms  10.388 ms  10.484 ms 
4  be-116-ar01.needham.ma.boston.comcast.net (68.85.106.29)  10.889 ms  10.620 ms  12.645 ms 
5  be-7015-cr02.newyork.ny.ibone.comcast.net (68.86.90.217)  18.580 ms  16.596 ms  17.417 ms 
6  hu-0-16-0-0-pe03.111eighthave.ny.ibone.comcast.net (68.86.86.234)  17.596 ms  16.427 ms  23.783 ms 
7  as15169-1-c.111eighthave.ny.ibone.comcast.net (23.30.206.122)  70.897 ms  70.864 ms  74.126 ms 
8  108.170.248.3 (108.170.248.3)  52.983 ms  61.882 ms 108.170.248.34 (108.170 .248.34)  34.967 ms 
9  216.239.58.111 (216.239.58.111)  19.614 ms 216.239.40.135 (216.239.40.135)  17.351 ms
... etc ...
```

**IMPORTANT!**: when selecting an ISP, low latency, not bandwidth, is more
important for optimizing speeds.  Latency is usually the performance bottleneck
for most websites.

---

**What makes fiber so special?**

Fiber optic cables can carry many different wave lengths of light in a process
known as _wavelength-devision multiplexing_ (WDM).  One fiber cable can
multiplex over 400 wavelengths making them an order of magnitude more effective
than copper/metal wires.

