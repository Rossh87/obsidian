# Merge intervals

URL: https://leetcode.com/problems/merge-intervals/submissions/

Categories:
1. 

Insights:
1. If we sort the intervals by begin time, we can build up a result and only ever need to interact with the final element of the result, instead of searching through the result array for each insertion.

Notes:

Solution:
```javascript
var merge = function(intervals) {
    if(intervals.length === 1) return intervals;
    
    intervals.sort((a, b) => a[0] - b[0]);
    
    const result = [];
    
    intervals.forEach(interval => {
        if(result.length === 0){
            result.push(interval);
            return;
        }
        
        const tail = result[result.length - 1];
        
        if(interval[0] > tail[1]){
            result.push(interval);
            return;
        }
        
        
        tail[1] = Math.max(interval[1], tail[1]);
    });
    
    return result;
};
```