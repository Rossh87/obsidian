An [[RPC]] (remote procedure call) is a paradigm of allowing code running in one process to invoke code in another process (even on a different host) as if it were a local function call.  gRPC is a Google-designed specification for implementing RPCs.

Messages in gRPC are usually encoded as [[Protocol Buffers]], a language/platform agnostic, lightweight, binary data encoding.  However, gRPC can can be configured to use other encodings, like JSON.

gRPC is popular for communcation between services in distributed/microservice architectures.  It has a good ecosystem in most popular languages.

Even though gRPC is approx. 5x faster than JSON, it requires access to lower-level [[TCP]] primitives that no browsers currently implement.