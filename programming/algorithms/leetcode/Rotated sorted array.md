# Rotated sorted array

URL: https://leetcode.com/problems/search-in-rotated-sorted-array/

Categories:
1. [[Binary search]] 

Insights:
1. Because the inconsistency caused by rotation only exists at one point in the array, every time the binary sort divides, at least one half of the array will be correctly sorted.
2. In general, if we have a binary choice to make, we only need *one* of the possible choices to be testable, since there's only one other option.

Notes:
Hardest part of binary searches is getting the midpoint selection right, and remembering that sort should run as long as left is less-that **or** equal-to right, not just less-than.  

Testing out midpoint selection on 1, 2, and 3 element lists should cover all cases.

Solution:
```javascript
var solve = function () {
    let left = 0;
    let right = nums.length - 1;
    let mid = 0;
    
    while(left <= right){
        mid = left + Math.ceil((right - left) / 2);
        
        const midVal = nums[mid];
        
        if(midVal === target){
            return mid;
        }
        
        if(midVal > nums[left]){
//             left side is sorted
            if(nums[left] <=target && midVal > target){
                right = mid - 1;
                continue;
            }
            
            left = mid + 1;
        } else {
//             right side is sorted
            if(target <= nums[right] && target > midVal){
                left = mid + 1;
                continue;
            }
            
            right = mid - 1;
        }
    }
    
    return -1;
}
```