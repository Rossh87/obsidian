# Find the duplicate number

URL: https://leetcode.com/problems/find-the-duplicate-number/

Categories:
1. [[Floyd's algorithm]]

Insights:
1. Every value in the array is necessarily a valid index of the same array.  This makes several approaches viable.
2. The best is probably to treat the array as a linked list with a cycle.  Use Floyd's algorithm to find the beginning of the cycle, and that will be one of the duplicated elements.

Notes:
Other approaches take advantage of the fact that array's values are also valid indices.  If it is acceptable to modify the array, we can swap each element to the idx of the array that corresponds to the elements value, and continue until we find an element whose idx value is already populated with itself.  When that happens we have the duplicate.  This can be done recursively or iteratively.  Since (in this problem) there is no element of value 0, we can start matching elements with their index at zero.

A final approach that may be useful for other problems is to visit the index corresponding to each elements absolute value, and set it to negative.  The first time we retrieve an element with a negative value, we know that index has already been visited, and that index corresponds to the duplicated value.

Solution:
```javascript
var findDuplicate = function(nums) {
    let slow = nums[0];
    let fast = nums[0]
    
    do {
        slow = nums[slow];
        fast = nums[nums[fast]];
    } while(slow !== fast)
    
    slow = nums[0];
    
    while(slow !== fast){
        slow = nums[slow];
        fast = nums[fast];
    }
    
    return slow;
};

// using array idx as value
var findDuplicate = function(nums) {
    const search = (n, val) => {
        const next = n[val];
        
        if(next === val){
            return val;
        }
        
        n[val] = val;
        
        return search(n, next);
    }
    
    return search(nums, 0);
}
// using array idx as value (same as above without recursion)
var findDuplicate = function(nums) {
    let next = 0;
    
    while(true){
        const tmp = nums[next];
        
        if(next === tmp){
            return next;
        }
        
        nums[next] = next;
        
        next = tmp;
    }
}

// set value at idx of current member to negative.  If it's already negative,
// we've found our duplicate
var findDuplicate = function(nums){
    for(let i = 0; i < nums.length; i++){
        const v = Math.abs(nums[i]);
        
        if(nums[v] < 0) return v;
        
        nums[v] = nums[v] * (-1);
    }
}
```