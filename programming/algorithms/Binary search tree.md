# Binary  search tree

A BST is a specialization of a [[Binary tree]] that is possible whenever the underlying data type is inherently ordered.  For any given node in a BST, every node in its left subtree is guaranteed to be less than the node itself, and every node in its right subtree is guaranteed to be greater than the node itself.  

Specializations of BST include [[red-black trees]] and [[AVL]] trees.  Both are instances of self-balancing trees, meant to limit the amount that mutations can skew the tree to the right or left, in the interest of maintaining good performance relative to the total number of nodes in the tree for future operations.