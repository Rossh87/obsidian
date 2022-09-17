# Embedding

Taken from https://eli.thegreenplace.net/2020/embedding-in-go-part-1-structs-in-structs/

## Structs in structs

*Embedding* a struct in another struct is mostly syntactic sugar.  In the following,
```go
type Inner{
	b int
}

type Outer{
	Inner
	a string
}

outerInstance := Outer{}

// this works
outerInstace.b = 4
```
`outer.b` is just a shorthand for, and behaves exactly the same as, `outerInstance.Inner.b`.  This is true for methods as well as properties.  In this example, `b` is considered a *promoted* field.

Note that when creating a struct literal that embeds another struct, we have to use an explicit struct literal for the embedded field (keys are optional as long as order is obeyed):
```go
outerLiteral := Outer{
	a: "some string",
	Inner: Inner{
		b: 42	
	}
}
```

If an embedding struct has fields or methods with the same name as fields or methods on the embedded struct, accessing those fields or methods on the embedder will refer to the appropriate reference for that name on the embedder, not the embeddee.  This is exactly as we would expect.  To access a *shadowed* field or method on the embeddee, call it explicitly as a property of the embedder:
```go
type Inner {
a string
}

type Outer {
Inner
a string
}

literalOuter := Outer{Inner: Inner{"inside"}, a: "outside"}

s1 := literalOuter.a // has value "outside"
s1 := literalOuter.Inner.a // has value "inside"
```

Promoted methods can satisfy interface.

## Interfaces in interfaces

This is the simplest embedding case.  The methods of an interface that embeds another interface are the union of the embedder's methods and the embeddee's methods.  

If the embedder has a method with the same name as a method of the embeddee, but a different function signature, it's a compiler error:
```go
type A interface {
	SharedWrong() string
}

type B interface {
	A
	SharedWrong() int //compiler error
}

type B interface {
	A
	SharedWrong() string //No problem--same signature as A.SharedWrong
}
```

## Interfaces in structs

Works identically to struct-in-struct, with one exception: the zero value of an interface is `nil`, unlike a struct, so we can get in trouble if we don't initialize the embedded interface with a concrete implementation.
```go
type Embedded interface {
	Foo() string
}

type Embedder struct {
	Embedded
}

bad := Embedder{} // So far so good, just a normal struct literal...

bad.Foo() // Bad.  Panics at runtime with a nil pointer dereferencing even though it compiles.  Notice 'Foo' is still promoted to the containing struct even though bad.Embedded is nil.

type Implementer struct {}

func(i Implementer) Foo() string{
	return "hello"
}

good := Embedder{Implementer{}}

good.Foo() // OK
```

Just like struct-in-struct, promoted methods on a struct that embeds an interface can satisfy another interface:
```go
type required interface {
	DoThing() string
}

func doer(req required) {
	req.DoThing()
}

// notice concrete has no DoThing() of its own, but embeds the 'required' interface
type concrete struct {
	required
}

type inner struct{}

func(i inner) DoThing() string {
	return "hello"
}


c := concrete{required: inner{}}

// compiles and runs: c satisfies 'required'
doer(c)
```

This is a surprisingly powerful tool when combined with method interception.  It allows us to write 'higher-order interfaces' that compose behavior without interfering with one another, and remain composable/relatively generic.  This is of course possible without the embedding syntax, but would require re-implementing all of the target interface's methods and explicitly delegating to the nested interface, rather than only shadowing the methods that need modification and allowing method promotion to keep the shadowing interface in compliance with the embedded interface.