# Slices
Slices provide a "window" onto an underlying array.  Unlike an array, which have a fixed length, slices can have variable length, but their capacity always comes from the array they are tied to.  

Multiple slices can be taken of the same array, but care must be taken in this case: because each slices refers to the same memory, changes to the elements of 1 slice will affect all others that share the same array.

If a slice is initialized via the literal syntax:
```go
s := []int{1,22,3}
```
its underlying array will have the same capacity as the contents of the initialized slice.  

The right-hand side of a slice can be re-sliced without affecting the underlying array. Below,
```go
s := []int{1,2,3,4}
//cap = 4
s = [:2]
//cap = 4
s = [:4]
//cap = 4, slice now contains all the elements it initially did.
```
re-slicing does not impact the array's capacity, and re-extending the slice to its original length allows us to recover all the elements from the original.  However, re-slicing the *beginning* (left-hand side) causes the array to lose capacity, and the elements are lost:
```go
s := []int{1,2,3,4}
//cap = 4
s = [2:4]
//cap = 2
s = [:6]
//PANIC--slicing beyond capacity.
```
This happens because slicing does not copy any data.  A slice is only a description of a certain array segment, consisting of a length, a capacity, and crucially a *pointer* to the first array element.  When the pointer is advanced, the head of the linked array data is lost, and the capacity of the slice and underlying array are diminished. 

The zero value of a slice is `nil`. A slice initialized like this:
```go
var s []int{}

empty := s == nil
//evaluates to 'true'
```
has length and capacity of 0, and no underlying array.  In contrast, a slice created with `make` has the specified length, and is filled with the appropriate zero value for its content type.  For example,
```go
s := make([]int, 5)
```
creates a slice of length 5, whose underlying array is of length and capacity 5, and that is filled with zeroes.  `make` accepts an optional third argument that allows setting a capacity for the slice independent of its length.

`append`ing to a slice silently handles the capacity of the underlying array for us.  If an append is requested that would exceed the capacity of the existing array, a new, longer array is created, the contents of the old array are copied, and a reference to the new array is returned. `append` increases capacity exponentially to avoid excessive reallocations as the array grows in size.

One potential gotcha with this implementation of slices is that, if a slice's backing array is very large, it will be persisted in memory for the life of the slice that looks into it.  Prevent this by creating a new slice of only the needed length and capacity, and copying the offending slice into it.