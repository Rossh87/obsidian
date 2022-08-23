# Combination sum

URL: https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

Categories:
1. [[Binary tree]]
2. [[Preorder traversal]]

Insights:
1. General idea is to arrange the right side of the tree so that traversing **as if it were the desired linked list**, i.e. moving strictly down the right-hand-side of the tree, will bring us into contact with nodes in the same sequence as a preorder traversal of the original tree.

Notes:
'Processing' a node consists of setting its left subtree to be the next node encountered, and setting its right subtree in a position to be encountered after the entirety of its left subtree.  So, we attach the entire left subtree to node's right (since that is the direction we will traverse), and then place any pre-existing right subtree at the bottom-right of the left tree, i.e. the position that will be encountered first once the entire left tree has been encountered.

Solution:
```javascript
var flatten = function(root) {
    if(!root){
        return root;
    }
    
    let currNode = root;
    
    while(currNode !== null){
        const l = currNode.left;
        const r = currNode.right;
        
        currNode.left = null;
        currNode.right = null;
        
        currNode.right = l;
        
        let bottomRight = currNode
        
        while(bottomRight.right !== null){
            bottomRight = bottomRight.right;
        }
        
        bottomRight.right = r;
        
        currNode = currNode.right;
    }
};
```