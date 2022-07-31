# First and last position of element in sorted array

URL: https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

Categories:
1. [[Binary search]] 

Insights:
1.  We can use normal binary search and just add criteria: instead of only checking identity of element, check that it has correct identity **and** that it is at the beginning or end of occurrences.
2. Binary search is O(log N) so searching twice is O(2 log N).  Drop the constant and we stay in O(log N).

Notes:

Solution:
```javascript
var solve = function () {

    if(nums.length === 0){
        return [-1, -1];
    }
    
    let targetStart = null;
    let targetEnd = null;
    
    let left = 0;
    let right = nums.length - 1;
    let mid = 0;
    
//     first binary search: find start
    while(left <= right){
        mid = left + Math.ceil((right - left) / 2);
        
        const midVal = nums[mid];
        
        if(midVal === target){
            if(mid === 0 || nums[mid - 1] !== midVal){
                targetStart = mid;
                break;
            } else {
                right = mid - 1;
                continue;
            }
        }
        
        if(nums[left] <= target && midVal > target){
            right = mid - 1;
            continue;
        }
        
        left = mid + 1;
    }

    if(targetStart === null){
	//if we didn't find any occurrences, we're done
        return [-1, -1];
    }
    
    left = 0;
    right = nums.length - 1;
    mid = 0;
    
    //     second binary search: find end
    while(left <= right){
        mid = left + Math.ceil((right - left) / 2);
        
        const midVal = nums[mid];
        
        if(midVal === target){
            if(mid === nums.length - 1 || nums[mid + 1] !== midVal){
                targetEnd = mid;
                break;
            } else {
                left = mid + 1;
                continue;
            }
        }
        
        if(nums[left] <= target && midVal > target){
            right = mid - 1;
            continue;
        }
        
        left = mid + 1;
    }
    
    return [targetStart, targetEnd]
}
```