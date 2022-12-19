A `var` is an alias for a memory address that has some value stored in it.  When we manipulate a variable, we are telling the CPU to do something to the contents of the memory address for which the variable is an alias.

A `pointer` is an alias for a memory address that *stores the memory address of another value*.  E.g. in the following:
```go
func main() {
	a := 2
	// 'b' is a pointer to 'a'
	b := &a
}
```
the memory block represented by `b` contains the memory address of the memory block assigned to a.  In the following sample, we see that we can use pointer `b` to manipulate the contents of `a`:
```go
func main() {
	a := 2
	b := &a
	// here we tell the program, 'give me a handle to
	//the memory block of the address stored in "a"'
	*b++	
	fmt.Println(a) // prints 3
}
```

Pointer arguments are not special.  When they are passed as an argument to a function, the value is *copied* into a new memory location inside the stack frame of the called function, just like any other type.  But because the contents do not change, the address stored in the *new* pointer still allows the called funtion to manipulate the contents of the stored memory address (i.e. the 4 or 8 bytes stored at that address, depending on system architecture). We can think of this as passing a pointer down the stack.

c.f. https://www.ardanlabs.com/blog/2017/05/language-mechanics-on-stacks-and-pointers.html

Returning a pointer, or passing a pointer *up* the stack, *is* a bit special.  Consider the following code:
```go
type user struct {
	name string
}

// returns a pointer
func newUser(name string) *user {
	u := user{"bill"}
	return &u
}

func main() {
	user := newUser()
}
```
When `newUser` returns inside of `main`, **all of the memory in the stack frame that had been allocated to the `newUser` call becomes invalid**. So `newUser` cannot return an address inside that range.  In order for the struct `u` to to be available inside of `main`, `u` must be allocated on the heap, and the returned pointer must point to that address.  The compiler determines at build time whether or not a value can be allocated on the stack or must be moved to the heap; this determination is called [[Escape Analysis]]