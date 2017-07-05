**Context-free Grammer**: the set of rules that describe all possible strings
in a given formal language.

**Extended Backus-Naur Form**: a meta-syntax notation which can be used to
express CFG programming languages.  Essentially, it's a language that can be
used to define other languages.  Useful when you want to define the 'rules' of a
language you're building in an easy to understand way.

**Compiler**: takes source code and converts it all into machine code.  Compiled
languages are generally harder to debug. Examples include: C, C++, Go, etc.

**Interpreter**: takes source and translates it one statement at a time. Takes
less time to analyze the source but slower to execution time. Examples include:
Ruby, Python, etc.

**Tree-walking interpreters**: these traverse the AST, visit each node and do
what the node signifies.  Often, these style of interpreters will have small
optimization steps before the eval.  For example, they might remove unused
variable bindings or turn the AST into a format that is easier for the
interpreter to consume.

Other interpreters will take the AST and convert it to bytecode which is an
intermediate representation (IR).  Bytecode is not real machine/assembly code
(although often looks very similar) rather it's code that is designed to be
executed by a Virtual Machine.  Just like VMWare will emulate real machines
these VM's emulate a machine that understands the bytecode format and can
execute it extremely fast.  The JVM is an example of this scenario.

**JIT**: the way JIT works is similar to above.  The steps are:  

1. Parse source code.
2. Build an AST
3. Convert the AST to bytecode
4. VM then compiles the bytecode to native machine code, **RIGHT BEFORE** it
   get's executed. Thus the "just-in-time" name.

**But why all the different techniques??**

_Strategy choice is depends on perfomance and portability needs_ A tree-walking
interpreter that recursively evaluates an AST is the slowest at execution time
but the easiest to build/reason about.  Generally, it appears the more perf you
need out of the language the harder and more time consuming the language design
tends to be.

## What does "Turing Complete" mean?
[Video explanation](https://www.youtube.com/watch?v=RPQD7-AOjMI)

What does a thing have to be to be turing complete?  

* needs to be able to do everything a turning machine can do.  
* must have conditional branching  
* must be able to read/write data  
* must have the ability to 'goto' somewhere different in memory (really just the essense of if/elses)  
* must be able to have abritrary amount of memory. (access to as much memory as the problem needs)  

A turing machine is an endless piece of tape (0/1's).  The ability to read and
write on an infinite piece of tape is powerful enough to compute anything.

## Article on Lisp/Developers by Paul Graham

>  If you chose technology that way, you'd be running Windows. When you choose
>  technology, you have to ignore what other people are doing, and consider only
>  what will work the best.

[Original article here](http://www.paulgraham.com/avg.html)
