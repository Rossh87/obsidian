# Binary search
Key Insight: If an algorithm depends on choosing between two paths, we only need ONE of those paths to be legible in order to make the choice.  e.g. in [[Rotated sorted array]], for each division only one of the two subdivisions is guaranteed to be in sorted order, but it doesn't actually matter: because we can rule the side we know to be sorted in or out, and there is only one other choice, we can proceed without adjusting for the unsorted side.

Sometimes called divide-and-conquer, a binary search works by repeatedly dividing the search space in half, then using the ordered nature of the stored values to determine which half should be used for subsequent searches.

Requires the searched data to be ordered and sorted.

Useful for arrays, but also other data structures like [[Binary search tree]]s.

When implementing binary searches, it is important to *run the search* even in the case the counters have met.  If a `while` loop is used, the condition should be something like:
```
while(left <= right) {
// note Math.ceil here--need this since left/right are zero-indexed
	mid = left + Math.ceil((right - left) / 2)
...logic
}
```
