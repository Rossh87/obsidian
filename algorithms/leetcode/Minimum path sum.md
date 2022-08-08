# Combination sum

URL: https://leetcode.com/problems/minimum-path-sum/

Categories:
1. [[Dynamic programming]]

Insights:
1. The minimal path to a given square must go through EITHER (row, col - 1), OR (row - 1, col).  So the minimal path sum is current square + the smaller of the two possible paths
2. Good candidate for dynamic programming, since the possible paths to (row, col - 1) and (row - 1, col) will go through many of the same squares

Notes:
Straightforward once we identify the three base cases:
1. top-left square, i.e. no movement, has exactly 1 unique path to itself
2. \[0, 1\] has exactly one unique path to itself (1 move to right from start)
3. \[1, 0\] has exactly one unique path to itself (1 move down from start)

Solution:
```javascript
const toKey = (row, col) => `${row},${col}`;

var minPathSum = function(grid) {
    const idx = new Map();
    idx.set(toKey(0, 0), grid[0][0]);
    
    const sumTo = (row, col) => {
        const existing = idx.get(toKey(row, col));
        
        if(typeof existing === 'number') return existing;
        
        let t1 = Number.POSITIVE_INFINITY
        let t2 = Number.POSITIVE_INFINITY
        
        if(row - 1 >= 0){
            t1 = sumTo(row - 1, col) + grid[row][col];
        }
        
        if(col - 1 >= 0){
            t2 = sumTo(row, col - 1) + grid[row][col];
        }
        
        const minTotal = Math.min(t1, t2);
        idx.set(toKey(row, col), minTotal);
        return minTotal;
    }
    
    return sumTo(grid.length - 1, grid[0].length - 1);
};
```

See also:
[[Unique Paths]]