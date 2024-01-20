TripleMake
==========

The 2 argument form of `make` can cause all sorts of fun bugs that can be
difficult to debug. This linter finds those uses and alerts you that perhaps
you should consider changing them to the 3 argument form to be more explicit.

An example
----------

```go
package main

import "fmt"

func main() {
	// Premature optimisation: we only want to put 5 items into this slice.
	test := make([]int, 5)

	// Oops!
	test = append(test, 1)

	fmt.Println(test) // [0 0 0 0 0 1]
}
```

A quick rant
------------

This is bad DX on the part of Go.
The difference between Length and Capacity of slices can be difficult to 
understand for the kinds of people who like to do premature optimisation,
and debugging this can be tricky too.