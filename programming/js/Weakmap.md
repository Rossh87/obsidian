IMPORTANT: Only accepts Objects or unregistered symbols as keys; most primitive data types don't have a lifetime and aren't garbage-collectable, so they can't be used as keys.

'Weak' because the reference from the map key to the underlying object is weak: it won't prevent the object referenced by the key from being garbage collected. Once the key is garbage collected, the value associated with the key can also be garbage collected, and it it no longer possible to recover the value: `.get(obj)` will return `undfined`.

They keys of a Weakmap are not enumerable (can't be listed).

Potentially useful for tracking metadata about an ephemeral object, e.g. a DOM element. Use the object as a key and track desired properties in the value. The use as a map key won't prevent the DOM object from being garbage collected, so the Weakmap can sit around in memory for the lifetime of the program having new objects associated with it and will never become a memory leak. The 'registration' code is relieved of the need to implement any cleanup. 