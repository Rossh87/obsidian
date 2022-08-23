# Maximum product subarray

URL: https://leetcode.com/problems/maximum-product-subarray/

Categories:
1. [[Kadane's algorithm]]

Insights:
1. By tracking the min and max possible values for each position, we can account for the possibility of negative elements
2. When we encounter a negative element, we get the maximum by multiplying the current element by previous *minimum*, not maximum.

Notes:

Solution:
```javascript
var maxProduct = function(nums) {
    const ln = nums.length;
   
    let maxProduct = nums[0];
    let prevMin = nums[0];
    let prevMax = nums[0];
    
    for(let i = 1; i < ln; i++){
        const currVal = nums[i];
        
        let currMin, currMax;
        
        if(currVal >= 0){
            currMin = Math.min(currVal, currVal * prevMin);
            currMax = Math.max(currVal, currVal * prevMax);
        } else {
            currMin = Math.min(currVal, currVal * prevMax);
            currMax = Math.max(currVal, currVal * prevMin);   
        }
        
        maxProduct = Math.max(currMax, maxProduct);
        prevMin = currMin;
        prevMax = currMax;
    }
    
    return maxProduct;
};
```