# Combination sum

URL: https://leetcode.com/problems/unique-paths/

Categories:
1. [[Dynamic programming]]

Insights:
1. Since robot can only move down or to the right, the number of unique paths to position \[row, col\]  is uniquePaths(row - 1, col) + uniquePaths(row, col - 1)

Notes:
Straightforward once we identify the base case:
top-left square, i.e. no movement, has exactly 1 unique path to itself.

Iterative approach makes it easier to realize that time and space complexity are O(m * n)

Solution:
```javascript
var uniquePaths = function(m, n) {
    const idx = new Map();
    
    idx.set('0,0', 1);
    
    const up = (row, col) => {
        const existing = idx.get(`${row},${col}`);
        
        if(existing !== undefined) return existing;
        
        let sum = 0;
        
        if(row - 1 >= 0){
            sum += idx.get(`${row - 1},${col}`) || up(row - 1, col);
        }
        
        if(col - 1 >= 0){
            sum += idx.get(`${row},${col - 1}`) || up(row, col - 1);
        }
        
        idx.set(`${row},${col}`, sum);
        
        return sum;
    }
    
    return up(m - 1, n - 1);
};

var uniquePaths = function(m, n) {
    const idx = Array(m).fill(null).map(() => Array(n).fill(0));
    
    idx[0][0] = 1;
    
    for(let row = 0; row < idx.length; row++){
        for(let col = 0; col < idx[0].length; col++){
            if(idx[row][col] !== 0) continue;
            
            const above = row - 1 < 0 ? 0 : idx[row - 1][col];
            const left = col - 1 < 0 ? 0 : idx[row][col - 1];
            
            idx[row][col] = above + left;
        }
    }
    
    return idx[m - 1][n - 1];
}
```