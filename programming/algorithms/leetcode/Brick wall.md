# Brick wall

URL: https://leetcode.com/problems/brick-wall/submissions/

Categories:
1. [[Prefix sum]]

Insights:
1. For the purposes of alignment, a gutter is uniquely identified by its distance from one or the other of the wall.  In this implementation, this means the sum of the list up to a given point.
2. The height of the wall - the number of segments in a given gutter gives us the number of layers a gutter line must pass through.  By subtracting the gutter with the most segments from wall height, we get the solution.

Notes:

Solution:
```javascript
var leastBricks = function(wall) {
// calculate and store prefix sum for each element of each row
    const idx = Array(wall.length).fill(null).map(() => []);
    
    for(let i = 0; i < wall.length; i++){
        const dest = idx[i];
        for(let j = 0; j < wall[i].length; j++){
            if(j === 0){
                dest.push(wall[i][j]);
                continue;
            }                            
            
            dest.push(dest[j - 1] + wall[i][j]);
        }
    }
    
//     count instances of each prefix sum
    const sums = new Map();
    let maxSegments = 0;
    
    for(let i = 0; i < idx.length; i++){
//         rightmost prefix doesn't count--we don't want right edge of wall to
//         be considered as a gutter
        for(let j = 0; j < idx[i].length - 1; j++){
            const pfx = idx[i][j];
            const existing = sums.get(pfx)
            
            if(existing === undefined){
                sums.set(pfx, 1);
                maxSegments = Math.max(1, maxSegments);
                continue;
            } 
            
            sums.set(pfx, existing + 1);
            maxSegments = Math.max(existing + 1, maxSegments);
        }
    }
    
    return wall.length - maxSegments;
};
```