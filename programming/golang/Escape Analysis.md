c.f. https://www.ardanlabs.com/blog/2017/05/language-mechanics-on-escape-analysis.html

Build-time step that determines whether a variable can be allocated on the current stack frame, or must go on the heap.  When a variable must be allocated on the heap, we say that it 'escapes'.

Stack memory is self-cleaning.  Heap memory is not, it must be managed by the garbage collector. Garbage collection is expensive, so it can be preferable to keep variables out of the heap. As an object grows in size, the garbage collection cost of allocating it on the heap may be outweighed by the cost of constantly copying it up and down the stack, so as usual, it depends.  This is relevant when deciding to use values or [[Pointer]] in functions and methods.

## Other Escapes
https://www.ardanlabs.com/blog/2017/06/language-mechanics-on-memory-profiling.html
1. Allocation sizes that are unknowable at compile time.  The compiler assigns the size of stacks at compile time, so if the size of something in a frame can't be determined until runtime, it will be allocated on the heap for safety.  A simple example is a [[Slice]] created like this:
```go
func doThing(input []byte) {
	// size of ouput is unknown until runtime--it will be placed on the heap
	output := make([]byte, len(input))
}
```
2. Assignment to an interface.  This happens because when a type is converted to interface, the compiler no longer knows its implementation details.  An interface accepted as an argument can do any arbitrary thing with data passed to its methods, including (e.g.) taking a pointer to something inside the callee and then trying to do something with it after the callee has returned.  