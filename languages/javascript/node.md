# Node 

## Why?
thread based web servers is a leaky abstraction that doesn't scale well.  I/O
needed to be thought about in a different way.  An event loop was Ryan's
solution.  JavaScript was already designed to work with an event loop in the DOM
and thus was a perfect fit.


