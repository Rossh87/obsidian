# Combination sum

URL: https://leetcode.com/problems/unique-paths/

Categories:
1. [[Dynamic programming]]

Insights:
1. Since robot can only move down or to the right, the number of unique paths to position \[row, col\]  is uniquePaths(row - 1, col) + uniquePaths(row, col - 1)
2. We can use [[Search Tree Pruning]] to eliminate recursive branches by memoizing
3. Finally, because we traverse grid predictably, we only need to track a single row in our memo array.

Notes:

Solution:
```javascript
var uniquePaths = function(m, n) {

if(m === 1 || n === 1) return 1;

const rows = m;

const cols = n;

  

const store = Array(n).fill(1);

  

for(let row = 1; row < rows; row++){

for(let col = 1; col < cols; col++){

store[col] = store[col - 1] + store[col];

}

}

  

return store[n - 1];

};
}
```