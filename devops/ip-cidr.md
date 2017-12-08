# CIDR  - Classless Inter-Domain Routing 

> It's called classless because before it was invented the 

When calculating how many IPs in a CIDR for IPv4
2^address length − prefix length

Address length is 32 for IPv4 and 128 for IPv6.

Subnet masks:

255.255.255.0 is the network mask for the 192.168.1.0/24 prefix

255.255.255.255 would be for /32

Ahh this is making sense. 32 bits split into 4 is 4 bytes.  Each byte maxes out
at 255 or 11111111. So 255.255.255.255 is 32 'ON' bits.

![Subnets](./subnets.png)
