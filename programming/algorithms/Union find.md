# Union find

Sometimes called a disjoint subset union, the union find data structure implements two methods:

1. `union` takes two subsets and forms a union of them.  If we have the set `{1}` and the set `{2}`, `union(1,2)` is `{1,2}`.  In this particular data structure, a single member of each subset is chosen to be the 'representative' of each distinct subset.  Different logic can be used to choose the representative: it could be largest/smallest, highest priority, etc.
2. `find` is used to determine the representative element of the subset to which a given element belongs.

The subsets within a union find are often represented as trees, with the root of the tree functioning as the representative for the given subset.

A common use of this algorithm is for finding the number of 'unique' somethings, where the uniqueness of a thing is determined by whether or not it is connected to any other thing, representable as the presence or absence of an edge in an undirected graph.  C.f. [[Number of connected components in undirected graph]].