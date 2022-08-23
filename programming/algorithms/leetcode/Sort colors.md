# Sort colors

URL: https://leetcode.com/problems/sort-colors/

Categories:
1. [[Sorting]]

Insights:
1. Since there are only 3 categories, we can deal with the two that belong on the ends by iterating the list once, and moving 0 and 2 to the correct end of the array whenever we encounter them.  Since 1 is between 0 and 2, sorting 0 and 2 will naturally cause 1 to cluster in the middle, so we can just skip any 1s we encounter.

Notes:
The tricky implementation bit is incrementing the index at the appropriate time.  We increment when we have added a zero, or when we are skipping a 1.  Logically, this means everything left of the idx is either a zero or a one, which means that anytime the idx has *passed* the zero boundary, the zero boundary itself is necessarily on a 1.  So we can always swap a zero under the index with whatever is under the zero boundary and immediately increment the index: either the idx and zero boundary are moving together over pre-existing leading zeroes, **or** we have swapped a 1 into the idx position, which we don't need to do anything special with.  Notice that we do NOT increment idx when we encounter a 2.  Instead, we keep swapping and decrementing the 2 boundary until we end up with a 1 or zero under the index, or we're done--whichever comes first.

'While' condition needs to run one more time when it equals the 2 boundary, since the boundary positions are always 1 position **inside** of the sorted 'bins'.

Solution:
```javascript
const swap = (p1, p2, arr) => {
    let tmp = arr[p1];
    arr[p1] = arr[p2];
    arr[p2] = tmp;
}

const RED = 0;
const WHITE = 1;
const BLUE = 2;

var sortColors = function(nums) {
    if(nums.length === 1){
        return;
    }
    
    const n = nums.length;
    
    let red = 0;
    let blue = n - 1;
    let idx = 0;
    
    while(idx <= blue){
        if(nums[idx] === RED) {
            swap(red++, idx++, nums);
        }
        
        else if(nums[idx] === WHITE){
            idx++;
        }
        
        else {
            swap(blue--, idx, nums);
        }
    }
};
```