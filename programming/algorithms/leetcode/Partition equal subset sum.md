# Partition equal subset sum

URL: https://leetcode.com/problems/partition-equal-subset-sum/

Categories:
1. [[Dynamic programming]]
2. [[Knapsack problem]]

Insights:
1. The target value (i.e. the 'weight limit' of our knapsack) is the sum of all elements in the array divided by 2.  If the total is not even, we know right away to return false.
2. To memoize the 'reachability' of a given amount, we need to store whether it is reachable *given a certain number of positions in the superset being chosen*.

Notes:

Solution:
```javascript
// iterative
var canPartition = function(nums){
    const total = nums.reduce((sum, next) => next + sum, 0);
    
    if(total % 2 !== 0) return false;
    
    const target = total / 2;
    
    const memo = Array(target + 1).fill(null).map(() => Array(nums.length).fill(null));
    
    memo[0].map(() => true);
    
    for(let amt = 1; amt <= target; amt++){
        for(let idx = 0; idx < nums.length; idx++){
            if(nums[idx] === amt){
                memo[amt][idx] = true;
                continue;
            }
            
            const takeTarget = amt - nums[idx];
            
            if(idx > 0 && takeTarget >=0 && memo[takeTarget][idx - 1]){
                memo[amt][idx] = true;
                continue;
            }
            
            if(idx > 0 && memo[amt][idx - 1]){
                memo[amt][idx] = true;
                continue;
            }
            
            memo[amt][idx] = false;
        }
    }
    
    return memo[target].some(el => el === true);
}

// recursive
var canPartition = function(nums) {
    const total = nums.reduce((sum, next) => next + sum, 0);
    
    if(total % 2 !== 0) return false;
    
    const target = total / 2;
    
    const memo = Array(target + 1).fill(null).map(() => Array(nums.length).fill(null));
    
    const dp = (amt, idx) => {
        if(amt === 0) return true;
        
        if(idx >= nums.length) return false;
        
        if(amt < 0) return false;
        
        if(memo[amt][idx] !== null) return memo[amt][idx];
        
        const result = dp(amt, idx + 1) || dp(amt - nums[idx], idx + 1);
        
        memo[amt][idx] = result;
        
        return result;
    }
    
    return dp(target, 0);
};
```