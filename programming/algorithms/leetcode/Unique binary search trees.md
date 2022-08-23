# Unique binary search trees

URL: https://leetcode.com/problems/unique-binary-search-trees/

Categories:
1. [[Catalan numbers]] 
2. [[Binary tree]]
3. [[Dynamic programming]]

Insights:
1.  If an array contains only unique integer elements between 1 and *N*, and array is of length *N*, the elements are necessarily all integers from 1 to *N*.  
2. Given the above, we can use any of the elements as the root and still be able to construct at least 1 valid BST with the remaining elements, if any.
3. The number of valid constructions for a given root is the number of valid constructions of the left subtree * the number of valid constructions of the right subtree
4. Loop over elements, calculate the number of valid constructions possible if we use the current element as the root, and add that number to a total to get the answer.

Notes:
Can be done iteratively (bottom-up) or recursively (top-down); in either case we use [[Dynamic programming]] and populate index with base cases 0 = 1 and 1 = 1.  Iterative approach requires populating the idx first with a double loop.

Without dynamic programming, solution has time complexity 2^N, since each call forks twice.  With dynamic programming, it should be (N^2).  More precisely, it should be O((N(N + 1) / 2).  This is clear from the index-building step of the iterative implementation: the outer loop runs N times, and each time adds one more step, yielding structure 1 + 2 + 3, + ... N that can be described as a particular type of [[List summation]].

Solution:
```javascript
// top-down recursive approach
var numTrees = function(n) {
    const idx = Array(n + 1).fill(-1);
    
    const recurse = (nodeCount) => {
        if(nodeCount < 2) return 1;
        
        if(idx[nodeCount] !== -1) return idx[nodeCount];
        
        let total = 0;
        
        for(let i = 1; i <= nodeCount; i++) {
            total += recurse(i - 1) * recurse(nodeCount - i);
        }
        
        idx[nodeCount] = total;
        
        return total;
    }
    
    return recurse(n);
};

// bottom-up iterative approach
var numTrees = function(n) {
    if(n < 2) return 1;
    
    const idx = Array(n+1).fill(-1);
    
    idx[0] = idx[1] = 1;
    
//     populate idx up to n
    for(let i = 2; i < idx.length; i++){
        let idxtotal = 0;
        for(let j = 1; j <= i; j++){
            idxtotal += idx[i - j] * idx[j - 1]
        }
        idx[i] = idxtotal;
    }
    
    return idx[n]
}
```