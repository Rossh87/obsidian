# Prefix sum
The prefix sum of a sequence of numbers is a second, parallel sequence whose members consist of the running total of the first sequence up to the given position.  Derivation is very simple:  given a sequence `x` and a prefix sum sequence `y`, `y[k] = y[k-1] + x[k]`.

Useful in some spatial algorithms for determining things like alignment or sameness between items.  See [[Brick wall]].