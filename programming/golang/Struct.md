# Structs

Unlike [[Map]] and [[Slice]], the zero value of a struct is not `nil`, but rather a struct with all of its values set to the appropriate zero value.  So, the below works perfectly well:
```go
type spkr struct{
	name string
}

func (s spkr) Speak() {
	fmt.Println("hello!")
}

var zeroedSpkr spkr

zeroedSpkr.Speak()
```