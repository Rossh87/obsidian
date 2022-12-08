# Subarrays

The precise number of subarrays possible to construct from an array of length `N` is caclulated as `(N(N - 1)) / 2` -- the same formula used to calculate the sum of consecutive integers.  The number of subarrays is equal to the number of subarrays of length `len` + subarrays of length `len - 1`, `len - 2`, ...etc.  Since there is only 1 possible subarray of length `len`, and 2 of length `len - 1`, we can see we are just adding consecutive integers starting at 1.  Note that this is on the order of `O(N ^ 2)` in terms of time complexity****.