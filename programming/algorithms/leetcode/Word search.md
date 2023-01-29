# Word search

URL: https://leetcode.com/problems/word-search/

Categories:
1. [[Depth-first search]]
2. [[Backtracking]]
3. [[Search Tree Pruning]]
4. [[Flood fill]]

Insights:
1. We can think of the decision-tree of this kind of algorithm as having each matrix element as a possible root, each root/subroot having 1 potential child for each adjacent and unused matrix element
2. We can prune potentially large parts of the decision tree by testing if a given candidate word is valid *so far*, which smacks of [[Backtracking]].

Notes:
Two tricky bits:
1. Be sure to 'pop' a candidate element from the 'used' array once all tests against it have been run
2. Getting the early return and short-circuiting working is tricky.  Make DFS return true/false, and use that to break outer loop

Solution:
```javascript
var exist = function(board, word) {
    const inBounds = (row, col) => {
        return row >= 0 && row < board.length && col >= 0 && col < board[0].length;
    }
    
    const dirs = [[0, 1], [0, -1], [1, 0], [-1, 0]];
    
	const used = Array(board.length).fill(null).map(() => Array(board[0].length).fill(false));
    
    const dfs = (row, col, idx) => {
        if(board[row][col] === word[idx]){
            if(idx === word.length - 1){
                return true;
            }
            
            used[row][col] = true;
            
            for(let m = 0; m < dirs.length; m++){
                const [dy, dx] = dirs[m];
                
                const nextRow = row + dy;
                const nextCol = col + dx;
                
                if(inBounds(nextRow, nextCol) && !used[nextRow][nextCol]){
                    const v = dfs(nextRow, nextCol, idx + 1)
                    
                    if(v) {
                        return true;
                    }
                }
            }
            
            used[row][col] = false;
            return false;
        }
        
        return false;
    } 
    
    for(let i = 0; i < board.length; i++){        
        for(let j = 0; j < board[0].length; j++) {
           if(dfs(i, j, 0)) return true;
        }
    }
    
    return false;
};
```