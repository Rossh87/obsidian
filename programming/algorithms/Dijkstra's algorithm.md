# Dijkstra's algorithm

This algorithm allows us to find the shortest distance between two nodes in an undirected or directed graph with positively weighted edges.  It is a greedy algorithm, eagerly selecting the shortest paths first.  There is a simple intuition behind this behavior: the shortest path to node `dest` from node `source` via node `inter` is necessarily the shortest path from `source` to `inter` + distance from `inter` to `dest`.

If the graph is represented as an [[Adjacency matrix]], we can find the minimum distance from any node to every other node in the graph in `O(V^2)` time and `O(V)` space with Dijkstra's alogritm.  The steps are as follows:
1. Given: an N x N adjacency matrix and a node identity `source`  (0 <= `source` < N)
2. Create array `distances` of size N, filled with `Number.POSITIVE_INFINITY`. `distances[i]` indicates the shortest distance path from `source` to `i`.
3. Create `Set<int>`  `sptSet` that stores the identity of nodes that have already been processed.
4. `distances[source]` = 0
5. While `sptSet.size` < N, find the next-closest node `minNeighbor` by iterating through `distances` and getting the idx of the smallest value.  `minNeighbor` represents the next node to be visited.  Add the node to `sptSet`, and then update `distances` for all nodes adjacent to `minNeighbor`.  The value of the adjacent node is `min(currentValue, distances[minNeighbor] + matrix[minNeightbor][adjacentToMinNeighbor])`
6. Continue until `sptSet.size` = N.  At that point, `distances` will be fully-populated with the shortest distances from `source` to `i`.

Note that with this algorithm, there is no need to visit  a node more than once: because of the greedy behavior described in the first paragraph, the first time we calculate the distance to a given node will be the shortest possible path. A node is considered 'visited' when it has been selected as the `minNeighbor`

The performance of the above implementation is `O(V^2)` time because we iterate over all `V` nodes `V` times in the process of looking for `minNeighbor`.

A more performant approach is possible by adding distances to a `minHeap` instead of storing them in an array.  In this implementation, we add a node to `sptSet` whenever it is popped from the `minHeap`, then add its neighbors to the `minHeap` with their total distance from the source.  If a node popped from `minHeap` is already in `sptSet`, we ignore it.  Likewise, if we encounter an edge pointing to a node that is already in `sptSet`, there is no need to re-add it to the heap: the path from the first time it was added to the heap will necessarily have been shorter. 