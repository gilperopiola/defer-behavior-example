## ————— (👁️_👁️)

```
package main

import (
	"time"
)

func main() {
	// This program calls fnWithDeferredGoroutine, which on defer spins up a goroutine that sleeps 1s and then prints '2'.
	// The main func will continue executing while the goroutine is sleeping, so it will print '1' before the '2' is printed.
	// After printing '1', the main func also sleeps for a while, giving the goroutine time to wake up and print the '2' before the program exits.
	// This will output: 012

	print("0")
	fnWithDeferredGoroutine()
	print("1")
	time.Sleep(2000) // If we remove this, then the '2' won't get printed as the program will exit and stop running goroutines.
}

func fnWithDeferredGoroutine() {
	defer func() {
		go func() {
			time.Sleep(1000)
			print("2")
		}()
	}()
}
