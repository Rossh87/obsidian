# Path sum III

URL: https://leetcode.com/problems/path-sum-iii/

Categories:
1. [[Prefix sum]]

Insights:
1.  A single path along a binary tree is equivalent to a 1-dimensional list, so the prefix sum technique should be able to be applied.

Notes:
The tricky edge cases here revolve around zeroes.  Don't add the current sum to the `occurences` data until right before proceeding the next level of the tree.  It's easier to think about the body of the recursive algorithm if we know `occurences` only contains data from previous levels.

Solution:
```javascript
// Just a helper structure for tracking prefix sums in O(1)
class Occurences {
    constructor(){
        this.map = new Map();
    }
    
    inc(num){
        const existing = this.map.get(num) ?? 0;
        
        this.map.set(num, existing + 1);
    }
    
    dec(num){        
        const existing = this.map.get(num);
        
        if(existing === undefined || existing <= 0) return;
        
        this.map.set(num, existing - 1);
    }
    
    count(num){
        const ct = this.map.get(num);
        
        if(ct === undefined) return 0;
        
        return ct;
    }
}

var pathSum = function(root, targetSum) {
    if(!root) return 0;
    
    const occ = new Occurences();
    
    let count = 0;
    
    const dfs = (node, pfx) => {
        if(!node) return;
        
        const currSum = pfx + node.val;
        
        if(currSum === targetSum) count++;

        count += occ.count(currSum - targetSum)
        
        occ.inc(currSum);
        
        dfs(node.left, currSum);
        
        dfs(node.right, currSum);
        
        occ.dec(currSum);
    }
    
    dfs(root, 0);
    
    return count;
};
```