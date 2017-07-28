# Client Side JS

JavaScript engine JavaScriptCore used AST walking and direct execution until
2008 when it switched to VM and bytecode.  It now has 4 stages of JIT
compilation which kick in at different times for various optimization reasons.
(from building interpreter in Go)

Was reading an article by Phillip Walton on how to become a great frontend
engineer and this quote stood out:

> When two or more browsers render the same code differently, you should take
> the time to figure out which one of them is correct and write your code with
> that in mind. Your workarounds will be far more future-proof as a result.

[Great article on setting up offline UX](https://mxb.at/blog/youre-offline/)
