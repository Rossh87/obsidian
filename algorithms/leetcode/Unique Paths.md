# Combination sum

URL: https://leetcode.com/problems/unique-paths/

Categories:
1. [[Dynamic programming]]

Insights:
1. Since robot can only move down or to the right, the number of unique paths to position \[row, col\]  is uniquePaths(row - 1, col) + uniquePaths(row, col - 1)

Notes:
Straightforward once we identify the three base cases:
1. top-left square, i.e. no movement, has exactly 1 unique path to itself
2. \[0, 1\] has exactly one unique path to itself (1 move to right from start)
3. \[1, 0\] has exactly one unique path to itself (1 move down from start)

Solution:
```javascript
const toKey = (row, col) => `${row},${col}`;

var uniquePaths = function(m, n) {
    const idx = new Map()
    idx.set(toKey(0, 1), 1)
    idx.set(toKey(1, 0), 1)
//     'no moves' = 1 unique path
    idx.set(toKey(0, 0), 1)
    
    const uniqueCount = (row, col) => {
        
        const existing = idx.get(toKey(row, col));
        
        if(typeof existing === 'number'){
            return existing;
        }
        
        let total = 0;
        
        if(row - 1 >= 0){
            const sub1 = uniqueCount(row - 1, col);
            idx.set(toKey(row - 1, col), sub1);
            total += sub1
        }
        
        if(col - 1 >= 0){
            const sub2 = uniqueCount(row, col - 1);
            idx.set(toKey(row, col - 1), sub2);
            total += sub2;
        }
        
        return total;
    }
    
    return uniqueCount(m - 1, n - 1)
}
```