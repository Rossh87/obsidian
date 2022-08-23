# DFS
Often applied to searching trees, but relevant in other situations as well (e.g. matrix-walking), a depth-first search completes a given choice-branch before moving to a different branch.  In a tree structure, this means walking all the way to the bottom of a given subtree before processing other subtrees.   

Recursive implementation is usually simplest, but can be done iteratively as well.

A depth-first approach can also be taken in [[Topological sorting]].  See below, taken from https://www.geeksforgeeks.org/topological-sorting/
![[Topological-Sorting-1.png]]
[[Kahn's algorithm]] can also be used to perform a topo sort, or to detect a cycle and invalidate a candidate graph from being a DAG.