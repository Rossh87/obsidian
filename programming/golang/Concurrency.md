# Concurrency

## Goroutines
Go handles concurrency via 'goroutines', which are lightweight threads managed by the Go runtime (as opposed to the OS scheduler).  Declare a concurrent operation using keyword `go`:
```go
func f (x, y int){
//do something here
}

go f(x, y, z)
```

In the above snippet, the *values* of `f, x, y, and z` are evaluated in the current goroutine, but `f`  is *executed* in a new goroutine.

Goroutines all operate on the same address space, so some mechanism for memory safety is required when multiple routines operate on shared data.

## Channels
Channels are a self-coordinating mechanism for orchestrating goroutines.  By default, an input instruction to a channel will block the current thread until the channel is able to receive the input, and an extract instruction from a channel will block until the data is ready to be extracted
```go
//split work of summing a slice between 2 goroutines
func sum(as []int, out chan) int {
	sum := 0

	for _, el := range as {
		sum += el
	}

	out <- sum
}

func main() {
	s:= []int{1, 7, 9, 22, 0, 4, 5}
	c := make(chan int)

	sum(:s[len(s) / 2], c)
	sum(s[len(s) / 2]:, c)

	//blocks until each extraction has finished and x and y are populated.
	//Note that without this line, the two functions executing in goroutines
	//would be blocked forever, since they cannot complete a 'push' instruction
	//until their is a 'read' instruction at the other end. In practice this causes 
	//a fatal 'deadlock' error.
	x, y := <-c, <-c

	fmt.Println(x + y)
}
```

Channel buffering lets us ease the blocking behavior of reading and writing to channels.  A buffered channel of size 2:
```go
c := make(chan int, 2)
```
Can be written to up to 2 times without any reading, and will not block.  Similarly, a buffered channel can be read from until it is empty before it blocks.  Overfilling a buffered channel, or reading from an empty one, causes a fatal deadlock error.

Senders can close a channel if the receiver needs to be notified when the sender is done sending values.  This is done by calling the built-in function `close` on the channel.  It is not necessary to close channels unless a specific implementation calls for it.  Once such implementation is 'iterating' over a channel's contents: the receiving code will block in the `range` loop until sender calls `close`.

`select` statements block until one of its cases can run, then executes that case.  For example, 
```go
c := make(chan int)
d := make(chan int)

select {
	case cVal := <- c:
		doThing(cVal)
	case dVal := <- d:
		doThing(dVal)
}
```
will call `doThing` with the contents of *either* c or d, whichever receives a message first.  If multiple cases can run, `select` chooses one of the available cases randomly.  Adding a `default` case to a `select` prevents the code from ever blocking: if a case matches it executes, otherwise the default executes immediately.

## Mutex
*Mutual exclusion*, or a mutex, is used when no communication is needed between goroutines, but memory safety is required for operating on shared data.  The standard library's `sync.Mutex` provides this functionality: all operations that affect shared data should refer to the same mutex.  By locking the mutex when the operation starts and unlocking it when it is done, conflict is prevented.  It is customary to wrap the mutex in question up in a struct, like so:
```go
// SafeCounter is safe to use concurrently.
type SafeCounter struct {
	mu sync.Mutex
	v  map[string]int
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
	c.mu.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	c.v[key]++
	c.mu.Unlock()
}

// Value returns the current value of the counter for the given key.
func (c *SafeCounter) Value(key string) int {
	c.mu.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	defer c.mu.Unlock()
	return c.v[key]
}

func main() {
	c := SafeCounter{v: make(map[string]int)}
	for i := 0; i < 1000; i++ {
		go c.Inc("somekey")
	}

	time.Sleep(time.Second)
	fmt.Println(c.Value("somekey"))
}
```