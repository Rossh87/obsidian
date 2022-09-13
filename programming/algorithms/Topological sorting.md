# Topological sorting

Directed acyclic graphs can be sorted such that, for every edge `uv` in the graph, `u` appears in the sorted order before `v`.  See https://www.geeksforgeeks.org/topological-sorting/ for example.

[[Kahn's algorithm]] is a breadth-first approach that is slightly fussier to implement due to the need to track the in-degree of each vertex, but makes cycle detection fairly easy:  If more nodes are processed than the number of vertices, a cycle exists.

[[Depth-first search]] combined with [[Postorder traversal]] yields a topo sort that is slightly simpler to implement: build an adjacency graph, perform a postorder traversal on each subgraph, and then reverse the output.  However, cycle detection is a bit more complicated:  it is necessary to track *both* whether a node has been visited or not, *and* whether it is part of the branch that is currently being traversed.  If recursion encounters a node that is marked as part of the current traversal branch, a cycle exists.