The classic form of this NP-complete problem is as follows:

Assume a backpack that can only carry a fixed amount of weight *W*, and a list of items, each of which has a *value* and a *weight*.  Calculate the set of items that maximizes the sum of their values, without exceeding the weight limit.

The optimal algorithm for this type of problem is a [[Dynamic programming]] approach that memoizes the *weights* from 0 to the maximum.  For every intermediate weight, we calculate the maximum value of the items that can be packed within that weight limit.  To do this efficiently, consider that the maximum value of a pack of weight `Wn` is `Max(value(Wn - W1) + V1), value(Wn - W2) + V2), value(Wn - W3) + V3)...`.  Thus, we can try each item with each weight and build up to a solution, or work top-down with a recursive solution with a very similar technique.

When building a dynamic programming solution from [[algorithms/leetcode/Subsets]], we can memoize by including information about how many of the available choices from the set have been made.  C.f. [[Partition equal subset sum]].