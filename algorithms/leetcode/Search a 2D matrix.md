# Search a 2D matrix

URL: https://leetcode.com/problems/search-a-2d-matrix/

Categories:
1. [[Binary search]]

Insights:
1. We can do two binary searches: one for the array that must contain target if it exists, and another for the target within that array

Notes:
As usual the tricky bit for me is remembering to correctly choose the 'middle' for each binary search.  In addition, the array-wise search has an extra 'if' condition: if the target falls within the range of the mid array itself, note the array somehow and terminate the search.  Otherwise, if target < mid\[0\], end = mid - 1; if target > mid\[length - 1\], start  = mid + 1

Solution:
```javascript
var searchMatrix = function(matrix, target) {
    const h = matrix.length;
    const w = matrix[0].length;
                                             
    if(target < matrix[0][0] || target > matrix[h - 1][w - 1]) return false;                                             
    
    let top = 0;
    let bottom = h - 1;
    
    while(top < bottom){
        const midArr = Math.floor((bottom - top) / 2) + top;
        console.log(top, bottom, midArr)
        
        if(matrix[midArr][0] <= target && matrix[midArr][w - 1] >= target){
            top = midArr;
            bottom = midArr;
            break;
        }
        
        if(target < matrix[midArr][0]){
            bottom = midArr - 1;
            continue;
        }
        
        top = midArr + 1;
    }
    
//     start and end are same at this point.
    const targetArr = matrix[top];
    let start = 0;
    let end = w - 1;
    
    while(start <= end){
        const mid = Math.floor((end - start) / 2) + start;
        
        if(targetArr[mid] === target) return true;
        
        if(targetArr[mid] > target){
            end = mid - 1;
            continue;
        }
        
        if(targetArr[mid] < target){
            start = mid + 1;
            continue;
        }
    }
    
    return false;
};
```