# Maps

Like [[Slices]] and pointers, the zero value of a map is nil.  A `nil` map has no keys, and no keys can be added to it. Under the hood, [a map is a pointer to an instance of `runtime.hmap`](https://dave.cheney.net/2017/04/30/if-a-map-isnt-a-reference-variable-what-is-it).  However, it cannot be dereferenced.

We can get a nil map like this:
```go
var nilMap map[string]string
```

Attempting to read from a `nil` map behaves like reading from an empty map.  e.g.:
```go
var m map[string]string

if el, ok := m["key"]; ok {
	//this won't run b/c 'ok' is false (nil pointer has no keys),
	//but it doesn't cause an error.
}
```

On the other hand, attempt to *write* to a `nil` map causes a panic:
```go
var m map[string]string

m["key"] = "uh-oh"
//Panics!
```

To avoid the panic, initialize the variable to a non-nil map using `make`:
```go
var m map[string]string

initialized = make(map[string]string)

// doesn't panic because we initialized map with call to 'make'
m["key"] = "good to go!"

if el, ok := m["key"]; ok {
	//this block executes now, and
	//'el' has the string value "good to go!"
}
```

Maps can also be initialized as literals.  The syntax is the same as a struct, except that the keys are always required:
```go
var m map[string]string

initialized := map[string]int{}

//NB we can still dynamically add keys, as with any other map. This doesn't
// panic, b/c we initialized the map as a literal above
m["third"] = 3
```

When indexing into a map, it is important to remember that the result of indexing into a non-existent key is **not** `nil` or some `undefined` equivalent, but rather the zero-value appropriate to the map's type.  This holds even when checking for the presence of a key using `ok`.; that is, the value of the variable declared in the checking syntax will be the zero value appropriate to the type of the map's values if the key is not present.