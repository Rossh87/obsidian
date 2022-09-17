# Search a 2D matrix II

URL: https://leetcode.com/problems/search-a-2d-matrix-ii/

Categories:
1. [[Staircase search]]
2. [[Binary search]]

Insights:
1. Basic staircase: If rightmost element of a row is too small, we know we have to go down 1 row.  Otherwise, go back a column.  This uses `O(M + N)` time.
2. With binary searching: for max efficiency, iterate `min(M, N)` times on the diagonal, performing binary search from `i` to the end on both the row and the column
3. The general insight is that, if a given cell is too large, **all** cells below and to the right of it will also be too large.  

Notes:

Solution:
```javascript

var searchMatrix = function(matrix, target) {
    const rows = matrix.length;
    const cols = matrix[0].length;
    
    if(target < matrix[0][0] || target > matrix[rows - 1][cols - 1]) return false;
    
    let row = 0;
    let col = cols - 1;
    
    while(row < rows && col >= 0){
        const el = matrix[row][col]
        if(el === target) return true;
        
        if(el < target) {
            row++;
            continue;
        }
        
        col--;
    }
    
    return false;
};
```