# Domain Name Sanity (notes on dns)

Figuring out if someone has registered a domain name:
```sh  
whois donkeyrentals.com
```

WHOIS privacy is not always worth it because it makes it so you can't prove that
you're the owner of the website.

## DNS Records:
`A` (for address) - always points to an IPv4 address like: `104.131.191.2`  

Examples:  
```
Host: @  
Record Type: A  
IP Adress: 104.131.191.2
```

@ means **apex domain** (aka bare, top, root, or naked domain) i.e.
donkeyrentals.com vs. www.donkeyrentals.com 

A Record with subdomain:
```
Host: accessories
Record Type: A
IP Address: 104.131.191.2
```
will map to accesories.donkeyrentals.com

AAAA records are the same as A but they point to IPv6 instead of IPv4.  IPv6
addresses look like this: `2620:0000:0861:ed1a:0000:0000:0000:0001`

**TIP**: To visit IPv6 addresses in your browser you can put them in brackets like this:
`http://[2620:0:861:ed1a::1]`  

`CNAME`s redirect one site to another.  Often people will cname `www` to their
host so that both www.mywebsite.com and mywebsite.com display the same content

It's preferable to use A records over CNAME when possible:

> Requesting a CNAME record is different. It looks up the record, sees that it’s a CNAME, looks at what the record is pointing toward, and then restarts the request. This will make requests take longer to get to our final, glorious IP address.

Looking up nameservers:
```
dig +short donkeyrentals.com NS
```
Nameservers are how all other records are looked up.  It's very important to
have these right first or nothing else will work.

All MX (mail records) must point to an A or AAAA record at the end of the day
(and therefore have an IP address backing it)

**Root Servers** - all domains start somewhere, root servers are where. There
are 13 in total (a - m)

Software called a `resolver` finds the proper domain by going through one step
at a time.

## `dig` Deep Dive

`dig` - Domain Information Groper.  By default dig will look up A records.  You
can look up different records by adding the record type as an argument to the
command.  

`+short` - display just the necessary information we're looking for.  
`+trace` - allows you to see all there servers being hit in the lookup process  
`-x` flag can be used to lookup domain names given some IP address  

TTL (time to live) - how long lookups will be cached  

`nslookup` - an alternative to dig when using windows machines  

## whois

When looking up domains with `whois` by prepending your search with 'domain' and
putting it in double quotes you'll get better search results:

> whois "domain google.com"

## host

Host is like dig but displays nice friendly responses:

```
host facebook.com
```

Response:
```
facebook.com has address 173.252.120.68  
facebook.com has IPv6 address 2a03:2880:2130:cf24:face:b00c::25de  
facebook.com mail is handled by 10 msgin.vvv.facebook.com.  
```

## ping & ping6
Used to check to see if a server is up and running.  Use `ping` for IPv4 and
`ping6` for IPv6 servers  

Ping will run forever until cancelling with ctrl + c.  If you want to specify a
number of times to ping you can use the `-c` flag:
```
ping -c 5 donkeyrentals.com
```

## Curl
You can use the `-I` flag with curl in order to return the HTTP headers

## Security (SSL/TLS)
**TLS**: Transport Layer Security  
**SSL**: Secure Sockets Layer  

Some CA's (Certificate Authority) are "root" CA's so we call them "Root
Certificate Authorities" and we call their certs "Root Certificates" 

This whole system uses PKI (public-key infrastructure)

Starts with a pub/priv key pair.  These are cryptographically matched. 

When we want a certificate from a CA, we generate a key pair  

### Using OpenSSL to create certs

```
openssl req -nodes -newkey rsa:2048 -keyout donkeyrentals_com.key -out donkeyrentals_com.csr
```

> The server should listen for connections on port 443. This is the conventional port for TLS connections. When we visit a site at https:// as opposed to http://, it will try to make a request using port 443 instead of the standard port 80.
