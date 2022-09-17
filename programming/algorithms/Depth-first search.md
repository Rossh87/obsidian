# DFS
Often applied to searching trees, but relevant in other situations as well (e.g. matrix-walking, any graph), a depth-first search completes a given choice-branch before moving to a different branch.  In a tree structure, this means walking all the way to the bottom of a given subtree before processing other subtrees.   

Recursive implementation is usually simplest, but can be done iteratively as well.

A depth-first approach can also be taken in [[Topological sorting]].  See below, taken from https://www.geeksforgeeks.org/topological-sorting/
![[Topological-Sorting-1.png]]
[[Kahn's algorithm]] can also be used to perform a topo sort, or to detect a cycle and invalidate a candidate graph from being a DAG.

If there is the possiblity of a cycle in the graph, a [[Hashset or map]] can be used to store nodes that have already been visited and prevent entering the cycle.

Because [[Breadth-first search]] is more hassle to implement than DFS, it can be a useful trick to track the current depth with a parameter to the recursive function.  If there is one node to process per-row of the tree, the length of the result so far can give useful information about the node currently being processed when combined with the current depth.