# Maximal square

URL: https://leetcode.com/problems/maximal-square/

Categories:
1. [[Dynamic programming]]

Insights:
1. A given island square is the bottom-right corner of an island of size *x + 1* if the square above it, the square to its left, and the square on a diagonal of up + left are all the bottom-right corner of squares of size *x*.
2. Otherwise, a given island square is the bottom-right corner of an island of the minimum of those three values, + 1.
3. If it's ok to modify the original matrix, we can store the needed values in the matrix itself as we iterate, giving us O(N) time and O(1) memory.

Notes:
If we're updating matrix in place, it's helpful to convert values to numbers.

Be very careful about the max tracking logic: need to be sure to increment the value for a cell from the minimum of its neighbors, and to use that incremented value for the final step of setting the new global side max.

Don't forget to square the side length before returning!!


Solution:
```javascript
const inBounds = (row, col, rows, cols) => row >=0 && row < rows && col >= 0 && col < cols;

var maximalSquare = function(matrix) {
    const rows = matrix.length;
    const cols = matrix[0].length;
    
    const dirs = [[-1, 0], [0, -1], [-1,-1]];
    
    let maxSide = 0;
    
    for(let row = 0; row < rows; row++){
        for(let col = 0; col < cols; col++){
            matrix[row][col] = parseInt(matrix[row][col], 10);
            
            if(matrix[row][col] === 1){
                let min = Number.POSITIVE_INFINITY;
                
                dirs.forEach(dir => {
                    const [dx, dy] = dir;
                    
                    let v = 0;
                    
                    if(inBounds(row + dy, col + dx, rows, cols)){
                        v = matrix[row+dy][col + dx];
                    }
                    
                    min = Math.min(v, min);
                });
                
                matrix[row][col] = min + 1;
                
                maxSide = Math.max(maxSide, min + 1);
            }
        }
    }
        
    return maxSide ** 2;
};
```