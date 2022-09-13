# Subsets

URL: https://leetcode.com/problems/subsets/

Categories:
1. [[Backtracking]]

Insights:
1.  Can be done iteratively by pushing elements to every subset of the last element (bottom-up)
2. Can also be done recursively: recursive function takes the current element and calls itself, and it omits the current element and calls itself

Notes:
Time complexity of both algorithms is 2^N, where n is the length of input set.  This is more clear in the recursive approach, where each recursive call branches twice, leading to a binary decision tree of depth N.

Solution:
```javascript
var subsets = function(nums) {
    const result = [[]];
    
    nums.forEach(num => {
        const boundary = result.length - 1;
        
        for(let i = 0; i <= boundary; i++){
            const next = result[i].slice();
            
            next.push(num);
            
            result.push(next);
        }
    });
        
    return result;
};

var subsets = function(nums) {
    const result = [];
    
    const bt = (idx, partial) => {
        if(idx === nums.length){
            result.push(partial.slice());
            return;
        }
        
        partial.push(nums[idx]);
        bt(idx+1, partial);
        partial.pop();
        bt(idx+1, partial);
    }
    
    bt(0, []);
    
    return result;
}
```