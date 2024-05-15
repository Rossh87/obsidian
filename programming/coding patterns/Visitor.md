This pattern is useful when you have a group of objects of (potentially very) different types that need to go through some common transformation or process, but the objects are so different that the algorithm to process each object type is also different. In a normal control flow, the processing function would have to make a type check on each ingested object to select the right transformation. 

The visitor pattern delegates the responsibility for calling the right process *to the objects themselves*. First, a `Visitor` object is declared that exposes a different method for processing each type of object. Then each object type to be processed implements a common interface with an `accept` method that accepts an instance of `Visitor` as its only parameter. Each object knows its own type, so `accept` can call the correct method on `Visitor` with `this`.

Clever and interesting, but really a good idea? Are type-guards and `if` statements actually harder to understand and more error-prone? I don't think so. The one potential caveat is the processing function might need a really big union type for its parameter, but... who cares?