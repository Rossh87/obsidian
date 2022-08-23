# Palindrome partitioning

URL: https://leetcode.com/problems/palindrome-partitioning/submissions/

Categories:
1. [[Backtracking]]
2. [[Dynamic programming]]

Insights:
1. Classic backtracking problem.  Try substring of every possible length, and if it is a palindrome, recurse over the remaining substring.
2. We can memoize the palindrome checking function to save a few iterations, though it's not hugely impactful (it seems)

Notes:
Palindrome memoization can be done in a couple of ways.  A 2-D array of booleans can tell us whether `idx[left][right]` is a palindrome, or we can use a hashmap with substrings as keys. 

Solution:
```javascript
var partition = function(s) {
    const result = [];
    
    const idx = Array(s.length).fill(null).map(() => Array(s.length).fill(null));
    
    const isPal = (left, right) => {
        if(idx[left][right] === null){
            if(left >= right){
                idx[left][right] = true;
            } else {
                idx[left][right] = isPal(left + 1, right - 1) && s[left] === s[right];
            }
        }
        
        return idx[left][right];
    }
    
    const backtrack = (str, startIdx, partial) => {
        if(startIdx >= str.length){
            result.push(partial.slice());
            return;
        }
        
        for(let i = startIdx; i < str.length; i++){
            const candidate = str.slice(startIdx, i + 1);
            
            if(isPal(startIdx, i)) {
                partial.push(candidate);
                backtrack(str, i + 1, partial);
                partial.pop();
            }
        }
    }
    
    backtrack(s, 0, []);
    
    return result;
};
```