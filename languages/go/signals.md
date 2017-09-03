# OS Signals
This section should really be in a more general section but since I wanted to
know how to control signals in Go specifically I decided to document here.

[This is a good article explaining dif of 'kill' options](https://major.io/2010/03/18/sigterm-vs-sigkill/)
[How signals work internally](https://unix.stackexchange.com/questions/80044/how-signals-work-internally)

`kill` sends a `syscall.SIGTERM` and adding the `-9` sends a `syscall.SIGKILL`.
When developing Go programs that need to be able to perform some cleanup logic
after being killed we can use a blocking channel like so:

```go
package main

import (
	"fmt"
	"os"
	"os/signal"
	"syscall"
)

func main() {
	signalChannel := make(chan os.Signal, 1)

	// os.Interrupt == syscall.SIGINT
	signal.Notify(signalChannel, os.Interrupt, syscall.SIGTERM, syscall.SIGQUIT)
	<-signalChannel
	fmt.Println("\n\n\tCleaning up program.")
	os.Exit(1)
}
```

