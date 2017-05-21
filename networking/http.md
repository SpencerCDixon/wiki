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
a

## Useful Headers 
`Content-Disposition` -  allows you to specify that a GET request should be returned as an attachment to be downloaded  
