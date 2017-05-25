# HTTP

## History

* was invented by Tim Berners-Lee (same guy who thought up the WWW)
* was invented in 1991 (1 year older than I am!)
*

### Shortcomings of HTTP 0.9
* had no way to send media other than hypertext (i.e. no content negotiation)
* had no way of sending meta data about the requests (no headers)

By 1.0 there was content negotiation and request/response headers to provide
extra meta data to clients and servers.  It makes more sense to think of HTTP as
_hypermedia transport_ but the HTTP name happened to stick.

## What is it?

**Stages/steps**:
* DNS resolution
* TCP connection handshake
* TLS negotiation (if https)
* dispatch of HTTP request

Great visual representation as to why latency is often the bottleneck:
![latency and bandwidth](./assets/latency-bandwidth.png)

The main thing to take away from this diagram is that at a certain point more
bandwidth doesn't provide much speed increase.  If you're ISP is delivery ~5Mbps
then you're about maxed out on bandwidth speed bumps and it's more important to
focus on latency.  Decreasing latency has a far more profound impact on the
speed at which a website is loaded.

SPDY which later turned into HTTP/2's main goal is to help fix this latency
bottleneck.  Either we need to improve the roundtrip time or reduce the number
of roundtrips in order to speed things up...

**Head of line blocking**: is when you have a resource that is finished
processing on the server but can't be sent back to the client because there is a
response still processing ahead of it in the queue.  This occurs in HTTP/1.x.
Imagine request for HTML/CSS... if the CSS finishes but the HTML is still
processing the CSS just has to sit in a buffer until the HTML is finished and
then it can be flushed.

## Useful Headers 
`Content-Disposition` -  allows you to specify that a GET request should be returned as an attachment to be downloaded  


**PLT** - Page Load Time aka the time it takes for the `window.onload` to be
called.

## Useful Tools
* [Useful for testing website speed and see the waterfall in various browsers](https://www.webpagetest.org/)



