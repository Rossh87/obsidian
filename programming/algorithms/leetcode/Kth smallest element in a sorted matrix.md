# Kth smallest element in a sorted matrix

URL:  https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/

Categories:
1. [[Binary search]]

Insights:
1. Binary search the **answer space**, not the elements of the matrix
2. Use a stairstep approach to count all elements >= a current target:  start with top right, and if element > target, decrement column.  Once element is encountered that's <= target, all elements directly to its left must also be <= target, so increment count by number of elements remaining in the row, jump down 1 row, and continue until we've been through all rows. 
3. ALTERNATIVE: since each row is sorted, we can basically do a merge sort without actually merging from the start of each row.  Use a [[Heap]] to track the current head of each eligible row.  Pop `k` times, and add the next element from the same row as the popped element to the heap.  Once we've gotten `k` elements from the heap, we're done.  Since columns are also sorted top-to-bottom, there's never a need to include more than `k` rows, so time complexity comes to `O(min(N, K) + K log(K))` 

Notes:
We can improve the efficiency a little bit by binary-searching through each row while we're gathering the count.

Solution:
```javascript
// Approach: binary search the *answer* space, counting number of elements
// that are less or equal to a candidate answer.  When we find a number that has k - 1
// elements smaller than or equal to itself, that number is necessarily the kth element
const kthSmallest = (matrix, k) => {
    const n = matrix.length;
    
//     bounds of the search space are set by smallest and largest el
//     in matrix
    let low = matrix[0][0]
    let high = matrix[n - 1][n - 1]
    
    while(low < high){
        const mid = Math.floor((low + high) / 2);
        
        const count = lessOrEqual(mid, matrix);
        
//         if # of elements <= candidate is < k,
//         we can rule out candidate--we def need a bigger number
        if(count < k){
            low = mid + 1;
        } else {
//             if # of els <= candidate is >= k, we might have the answer,
//         but it might be something smaller, so rule candidate in, but rule out
//             everything larger
            high = mid;
        }
    }
    
    return low;
}

const lessOrEqual = (target, matrix) => {
    const n = matrix.length;
    
    let row = 0;
    let col = n - 1;
    let count = 0;
    
    while(row < n && col >= 0){
        if(matrix[row][col] <= target){
            count += col + 1;
            row++;
        } else {
            col--;
        }
    }
    
    return count;
}
```