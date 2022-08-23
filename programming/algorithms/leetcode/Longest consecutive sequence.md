# Longest consecutive sequence

URL: https://leetcode.com/problems/longest-consecutive-sequence/

Categories:
1. [[Hashset or map]] 

Insights:
1. KEY insight that takes us from O(N ^ 2) to O(N) is that we can programatically determine whether or not a given element is the beginning of a sequence, and ignore it if it is not.  Do this by checking whether list contains val - 1.
2. To enable this, we also have to convert list elements to a structure with better lookup efficiency (hash table, Set, w/e)

Notes:
Once we've identified the beginning of a sequence, setting a base increment and increasing it in a `while` loop is an elegant way to check for presence of subsequent members of sequence.

Solution:
```javascript
var longestConsecutive = function(nums) {
    let ct = 0;
    
    if(nums.length === 0){
        return ct;
    }
    
    const idx = new Set(nums);
    
    for(let i = 0; i < nums.length; i++){
        const num = nums[i]
//         if this is true, the current number can't be the beginning
//         of a sequence, so there's not reason to check further
        if(idx.has(num - 1)){
            continue;
        }
        
        let ln = 1;
        let inc = 1;
        
        while(idx.has(num + inc)){
            ln++;
            inc++;
        }
        
        ct = Math.max(ln, ct);
    }
    
    return ct;
};
```