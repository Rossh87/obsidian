# Binary tree right side view

URL: https://leetcode.com/problems/binary-tree-right-side-view/

Categories:
1. [[Depth-first search]]
2. [[Breadth-first search]]

Insights:
1.  Take the rightmost node of a given level.

Notes:
Iterative breadth-first search here is tricky because we need to traverse each level from left to right, which is tricky without using `shift`, which is very unperformant.  A first-in-first-out (queue) structure is what is needed.

Solution:
```javascript
var rightSideView = function (root) {
    const ans = [];
    
    const dfs = (node, answer, depth) => {
        if(node === null){
            return;
        }
        
        if(depth === answer.length){
            answer.push(node.val);
        }
        
        dfs(node.right, answer, depth + 1)
        dfs(node.left, answer, depth + 1)
    }
    
    dfs(root, ans, 0);
    
    return ans;
}
```