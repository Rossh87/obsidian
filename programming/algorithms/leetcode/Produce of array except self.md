# Produce of array except self

URL: https://leetcode.com/problems/product-of-array-except-self/

Categories:
1. [[Prefix sum]]

Insights:
1. If we calculate all prefix products (product of all elements up to position `i` for all `i`) and all postfix products (same as prefix, but iterating over list backwards), we can multiply `prefix[i-1]` with `postfix[i+1]` to get product-except-self for any index.
2. We only need to pre-generate either postfixes or prefixes, since we can keep track of the other at the same time as setting our result array.

Notes:
For the purposes of this question, O(1) memory means no auxiliary memory *except* the result array.  This is dumb IMO, but we can meet the requirement by storing prefixes in the result array, then overwriting it as we calculate postfixes.

The tricky bit is setting temporary variables at the appropriate time.  Be very thoughtful about this.

Solution:
```javascript
var productExceptSelf = function(nums) {
    const result = [];
    let prefix = 1;
    let postfix = 1;
    
    for(let num of nums){
        result.push(num * prefix);
        
        prefix = num * prefix;
    }
    
//     result now contains all prefixes--overwrite them backwards
    for(let i = result.length - 1; i >= 0; i--){
        if(i === 0){
            prefix = 1;
        } else {
            prefix = result[i - 1];
        }
        
        result[i] = prefix * postfix;
        
        postfix *= nums[i];
    }
    
    return result;
};
```