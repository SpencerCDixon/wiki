# Learn Bash The Hard Way

Notes from reading the book...


### Globbing

`*` - match all
`?` - match any single character
`[abd]` - matches any character from a, b, or d
`[a-d]` - matches any character from a, b, c, or d

### Variables

**Caps convention**  
VARIABLE=value

**Multi word variables**  
VARIABLE="multi word value"

**Requires double quotes for referencing other values**  
VARIABLE="using $OTHERVALUE in assignment"

**Special Variables**
`$PPID` - parent process id

These cannot be overwritten.  They are `readonly` variables.  You can set a
readonly variable like:

```sh
$ readonly MYVAR=mystring
```

For historical reasons, the backtick form is still very popular, but I prefer
the `$()` form because of the simplicity of managing nesting. You need to be
aware of both, though, if you are looking at others’ code!

> Prefer $() over ``

```sh
$ set -o errexit23 
$ set -o xtrace
```

Same as:
```sh
set -ex
```

Put curly braces around variables names in bash.
