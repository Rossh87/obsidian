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
	// here we tell the program, 'give me the memory block of the address stored in "a"'
	*b++	
	fmt.Println(a) // prints 3
}
```