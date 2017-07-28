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

[This is a great article explaining how pointers work in
Go.](https://dave.cheney.net/2017/04/26/understand-go-pointers-in-less-than-800-words-or-your-money-back)

## API Configuration -- using function options

[Great blog post explaining the pros/cons](https://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis)
[Rob pike explaining function options](https://commandcenter.blogspot.com.au/2014/01/self-referential-functions-and-design.html)
