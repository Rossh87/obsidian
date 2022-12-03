A strongly-typed, language-agnostic data format.  Message types as well as client and server methods are described by `.proto` files.  Codegen tools for the appropriate language can then automatically create data access and exchange classes (called a 'client stub') for whatever language is desired, making it possible for services written in different languages to communicate seamlessly, without any extra developer work.

Proto buffers are a very efficient encoding format, much faster than JSON.  

Proto buffers use [[Http 2]] multiplexing to accomodate multiple data streams over the same [[TCP]] connection, reducing overhead.