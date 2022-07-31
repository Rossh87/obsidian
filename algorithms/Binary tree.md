# Binary trees
A binary  tree is a specialization of the general [[tree]] structure, consisting of a root node, with a maximum of two child nodes.  Each child node is also limited to two children.

There are several (not mutually-exclusive) subshapes of binary tree:
1. A *full* binary tree is a binary tree in which each node has either 0 or 2 children
2. A *complete*  binary tree has every level full except possibly the last, and each child is as leftward as possible.  Note that the last left node is not required to have a right sibling; a complete binary tree is not necessarily a full binary tree.
3. In a *perfect* binary tree every leaf node is at the same level
4. In a *balanced* binary tree, the height of the tree is log N, where N is the number of nodes.  For this to be possible, the distance between the height of left and right subtrees of any given node can be no more than 1. 
5. *Pathological* or *degenerate* trees have no more than one child for any node in the tree.  If each node has only a left child, the tree is said to be skewed left.  Likewise for right.

The *balance* of a tree has performance implications.  A balanced [[Binary search tree]] has O(log N) performance for search, insert, and delete operations.  In contrast, a degenerate tree has no better performance than a linked list.