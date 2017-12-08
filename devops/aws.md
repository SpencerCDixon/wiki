# AWS Notes

**VPC** - Virtual private cloud.  When designing infrastructure you can think of
this like your city.  Inside the city we'll have separate zip codes or subnets.

**Subnet** - a masked bit on our IP range for storing separate chunks of
functionality.  For example:

```sh
10.0.0.0/24 - Public Subnet for Web Servers (10.0.0.0 - 10.0.0.255 256 IPs)  
10.0.1.0/25 - Private Subnet for API Servers (10.0.1.0 - 10.0.1.127 128 IPs)  
10.0.1.128/26 - Database Subnet for DBs (10.0.1.128 - 10.0.1.191 64 IPs)  
10.0.1.192/26 - Spare Subnet (10.0.1.192 - 10.0.1.255 64 IPs)  
```

> Note: In each subnet, AWS reserves 5 IPS, the first 4 and the final. So in our public subnet, it'd be 10.0.0.0, 10.0.0.1, 10.0.0.2, 10.0.0.3 and 10.0.0.255.

[Useful subnet calculator](https://www.ipaddressguide.com/cidr)

So subnets allow us to separate our city into separate neighborhoods.  The next
step is to define the roads allowing traffic to enter/exit different
neighborhoods. We do that with Route Tables:

> A Route Table is just a list of CIDR blocks (IP ranges) that our traffic can leave and come from.

> A subnet is associated with a Route Table and the Route Table dictates what traffic can enter and leave the subnet.

### Resources

* [understanding VPCs](https://start.jcolemorrison.com/aws-vpc-core-concepts-analogy-guide/)
