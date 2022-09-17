-Available in [[Http 1.1]] to address issues with streaming/pipelining of requests
-Specified by `Transfer-Encoding` header (value is 'chunked')
-Importantly, [[Http 2]] does not support this value for `Transfer-Encoding`.  It uses other mechanisms for managing streaming data.

Chunked transfer encoding works by including leading bytes for each chunk that indicate the size of the chunk to be expected.  When the client receives a chunk of size 0, it knows that the current response has finished.