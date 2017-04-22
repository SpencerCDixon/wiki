# Go

**When to use methods vs. funcs?**
Prefer using funcs when a calculation is idempotent and not going to affect any
state.  If a function has a dependency or intention of changing some state than
it makes sense to define it as a method on a type/struct.  In general, avoid
overuse of methods, as Steve Francia points out, most novice Go users tend to do
due to their backgrounds in OO.
