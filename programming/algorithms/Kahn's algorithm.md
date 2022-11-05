# Kahn's algorithm

Used for [[Topological sorting]] of DAGs, it often comes into play in problems that involve the notion of dependency.

General idea is as follows:
1. Measure the in-degree (i.e. the number of incoming edges) of each node in the graph.  
2. Enqueue all nodes with in-degree of zero.  It is important the storage structure used be a true queue, i.e. that it has a first-in-first-out behavior: this algorithm depends on a breadth-first traversal.
3. Dequeue a node, increment the processed node count, optionally do something to actually process the node (e.g. add it to the topo-sorted list we may be keeping), and decrement the in-degree of all its adjacent nodes.  If a neighbor's in-degree drops to zero, add it to end of the queue.
4. When queue is empty, if the number of processed nodes matches the total number of nodes, the DAG was valid and the sort is legitimate.  Otherwise the DAG was invalid.