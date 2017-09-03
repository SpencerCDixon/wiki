# Go

**When to use methods vs. funcs?**
Prefer using funcs when a calculation is idempotent and not going to affect any
state.  If a function has a dependency or intention of changing some state than
it makes sense to define it as a method on a type/struct.  In general, avoid
overuse of methods, as Steve Francia points out, most novice Go users tend to do
due to their backgrounds in OO.


## Pointers vs. Values
> A pointer is a variable that holds the memory address of another variable.

The `&` symbol can be thought of as: 'Address of'.

[This is a great article explaining how pointers work in Go.](https://dave.cheney.net/2017/04/26/understand-go-pointers-in-less-than-800-words-or-your-money-back)

## API Configuration -- using function options

[Great blog post explaining the pros/cons](https://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis)
[Rob pike explaining function options](https://commandcenter.blogspot.com.au/2014/01/self-referential-functions-and-design.html)

Testing Notes:
* test helpers should never return an error
* they should have access to the 't' variable and fail the test if there is an error
* for complex structs create an internal testString() string func to help with comparisons

## Concurrency

Go routines are allocated 2kb of memory and can grow as needed.  They are
multiplexed onto native OS threads.

Situations that would benefit from goroutines:

1. Fetching data from multiple external API sources (multiple HTTP requests)
2. Independent processing (fetching contacts and calendar data - distinct sources) 
3. Composition (Example by Twitter: Trends, Feed, Who to Follow)

_The easiest way to think of channels it to compare them to network sockets._

* two apps can connect over a network socket
* depending on how htey're written traffice can flow in one _or_ two directions (think websockets for example)
* sometimes the network conns are short-lived, othertimes they stick around a while
* any data can be sent on the network connections it just has to be marshalled into raw bytes

Go channels work like sockets between goroutines in a single app. Biggest
benefit is they are 'typed sockets' meaning you can send Go Structs through them
and the data doesn't have to be marshalled into raw bytes
