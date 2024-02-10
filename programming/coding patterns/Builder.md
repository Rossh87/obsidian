If a single class has many configurations, OR several classes have the same configuration interface, but not every possible configurable value is needed by every instance, builder pattern may be helpful. Declare the object type to be built methods that configure different aspects of the object. For example, `class House` might expose methods `buildWalls` and `buildChimney`--not every house will need a chimney. Business rules about configuration lives in these `build` methods.

Client code that needs an instance of a class is free to configure whatever parts of it are needed and leave the rest. In addition, different classes can expose the same 'buildable' interface with potentially different business rules, which hides the differences from client code, potentially making code more reusable.

Another interesting use case [here](https://refactoring.guru/design-patterns/builder), where two very different types of things (a car and its manual) should go through exactly the same configuration process. That is, the director code for a given type of car (e.g. 'SUV') can construct a well-configured car, and a corresponding well-configured manual, with the same set of instructions provided `Car` and `Manual` have identical `Builder` interfaces.

Use when:
1. You would otherwise need a constructor with a lot of overloads or a lot of optional parameters
2. A single product has multiple representations. Code that operates on a builder interface can then use all the different representations interchangeably
3. Construction steps need to happen at different times

NB:
The BUILDER requires a common interface, *not* the built products. In the example above, `Car` and `Manual` may have nothing in common. When this is the case, the builder interface can't declare the 'fetch result' method b/c its return type is not knowable in advance, and each implementation of `Builder` will need to declare its own 'fetch result' method. However, if the returned products are in the same hierarchy, it may be possible to define the fetch method on the `Builder` interface and have it return a supertype for all possible products.