# Validate binary tree

URL:  https://leetcode.com/problems/validate-binary-search-tree/

Categories:
1. [[Binary search tree]]

Insights:
1. The key to one approach is simply to remember the relationship between a BST and ordered-ness:  if we traverse the tree in-order, we should encounter values in strictly increasing order.  If we meet a value that's <= the previous value, the tree is invalid.
2. The key to a second approach is to image that, as we move down the trees branches, we are update a ceiling and a floor for what the next node can be.  The root node can have any value, but when we go down the left subtree, we *lower* the maximum value a node can have.  Likewise, when we go down the right subtree, we *increase* the minimum value a node must have.

Notes:
It's very important to keep in mind with BSTs that we CANNOT just check the relationship between nodes and their immediate children: the whole subtree must meet the min/max requirements imposed by the root.

"Normal" iterative and recursive approaches need O(N) time and O(N) memory.  If it acceptable to modify the tree, we can reduce auxiliary memory to O(1) by using a Morris traversal.

Solution:
```javascript
var isValidBST = function(root) {
    const stack = [];
    let currNode = root;
    let prev = null;
    while(stack.length > 0 || currNode !== null){
        while(currNode !== null){
            stack.push(currNode);
            currNode = currNode.left;
        }
        
        const n = stack.pop();
        
        if(prev !== null && n.val <= prev){
            return false
        }
        
        prev = n.val;
        
        currNode = n.right;
    }
    
    return true
}

var isValidBST = function(root){
    const check = (node, min, max) => {
        if(node === null) return true;
        
        if(node.val <= min || node.val >= max) return false;
        
        return check(node.left, min, node.val) && check(node.right, node.val, max);
    }
    
    return check(root, Number.NEGATIVE_INFINITY, Number.POSITIVE_INFINITY)
}
```