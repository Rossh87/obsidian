# Dynamic programming

Dynamic programming is a way to optimize recursive solutions solve the same subproblem more than once.  Archetypal example is a program that calculates the Nth Fibonacci number.  The solution can be calculated by recursing on N - 1 and N - 2; the resulting decision tree is a binary tree of depth N, giving a time complexity of O(2 ^ N).  Since the recursion is a depth-first traversal, the recursive function will be called with many values on its traversal of right subtree that it has already encountered while traversing left subtrees.  This makes is a good candidate for a dynamic approach.

By using some auxiliary memory to store results of calculations while recursing, we can eliminate many branches of the decision tree by retrieving the result for a given input, obviating subsequent recursion and reducing time complexity to O(N) in exchange for O(N) memory usage.  Because algorithms of exponential time complexity become unworkably slow very quickly, and because memory is relatively cheap in most modern computint environments, this is almost always a good trade-off.

Tip:  the number of entries in the `memo` structure give good hints about how the time complexity of the algorithm can be calculated.

Tip: It is important to be careful about ordering the check for a memoized value and the terminating condition in a recursive dynamic programming problem.  If the boundary condition is an input that is out-of-range for the dynamic programming store, but the code checks for a dp entry first, the code will throw.