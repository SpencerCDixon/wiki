# Client Side JS

JavaScript engine JavaScriptCore used AST walking and direct execution until
2008 when it switched to VM and bytecode.  It now has 4 stages of JIT
compilation which kick in at different times for various optimization reasons.
(from building interpreter in Go)
