# Permutation

A permutation is simply a re-ordering of the items in a set.  E.g., `{3,2,1}` is a permutation of the set `{1,2,3}`.

Permutation can either allow or disallow re-using of elements.

If re-use is allowed, calculating the number of permutations is very simple: multiply the number of items to choose from by the number of available positions.  For example, a combination lock with 3 dials has `10 x 10 x 10` permutations.  Generalizing, choosing `r` of something with `n` different types yields `n^r` permutations when re-use is allowed.

If items must be unique, then each choice reduces the number of possible choices for the next item, so for `n` types of item, the number of permutations is given by `n!` (`n x n - 1 x n - 2,... x 1`).  If `r` elements are to be selected, we add a division step to remove excess elements:
```
n! / (n - r)!
```
