# Search a 2D matrix II

URL: https://leetcode.com/problems/search-a-2d-matrix-ii/

Categories:
1. [[Staircase search]]

Insights:
1. If rightmost element of a row is too small, we know we have to go down 1 row.  Otherwise, go back a column.

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