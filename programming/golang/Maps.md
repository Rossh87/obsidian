# Maps

Like [[Slices]] and pointers, maps are a reference type, so the zero value of a map is nil.  A `nil` map has no keys, and no keys can be added to it.  Attempting to read from a `nil` map behaves like reading from an empty map.  e.g.:
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

m = make(map[string]string)

m["key"] = "good to go!"

if el, ok := m["key"]; ok {
	//this block executes now, and
	//'el' has the string value "good to go!"
}
```

Maps can also be initialized as literals.  The syntax is the same as a struct, except that the keys are always required:
```go
m := map[string]int{
	"first": 1,
	"second": 2,
}

//NB we can still dynamically add keys, as with any other map
m["third"] = 3
```

When checking for the presence of a key using `ok`, it is important to remember that the first return value will be populated even if the key was not present in the map.  It will be the zero value appropriate to the type of the map's values.