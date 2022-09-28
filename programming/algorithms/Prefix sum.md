# Prefix sum
The prefix sum of a sequence of numbers is a second, parallel sequence whose members consist of the running total of the first sequence up to the given position.  Derivation is very simple:  given a sequence `x` and a prefix sum sequence `y`, `y[k] = y[k-1] + x[k]`.

Common use case is to determine continuous subset sum/product in an array.  The simplest case is a 1D array.  Consider:
```javascript
const list = [1, 3, 4, 5, 8];

const prefixSums = [1, 4, 8, 13, 21];

const contiguousSubsetTarget = 9;
```

We can count the number of congiuous subsets in `O(N)` by tracking at the same time we build the prefix sum list:
1. Whenever we calculate a new prefix sum for index `n`, one of two things must be true if `n` represents the end of a valid contiguous sum:  either the valid subarray starts at idx 0, or it starts at some index after 0.
2. If valid subarray starts at 0, then the current prefix sum will be equal to the target.  If that's the case, increment count.
3. If valid subarray starts after 0, then some previously-calculated prefix sum must be equal to `currPrefix - target`.  If that's the case, increment count *as many times as the needed prefixSum has occured*.
C.f [[Path sum III]]

Also useful in some spatial algorithms for determining things like alignment or sameness between items.  See [[Brick wall]].