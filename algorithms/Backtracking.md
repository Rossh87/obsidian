# Backtracking

Backtracking is an approach to brute-force solutions that allows short-circuiting, sometimes allowing backtracking algorithms to complete in less time than a pure brute-force approach.

Problems for which it is possible to construct a partial solution and validate it are good candidates for backtracking, provided no other, more efficient approach exists.

One way to think of backtracking is as a kind of [[Depth-first search]].  The code path of a backtracking function can be described as a tree, and the backtracking algorith traverses the search space in depth-first order.