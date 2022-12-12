A context is a set of access parameters for [[kubectl]].  It consists of [[Cluster]], a user, and a namespace.  A context is the way a particular user can access a namespace within the specified cluster.

A simple way to think about this is that the current context controls 'who' `kubectl` is considered to be at the time.