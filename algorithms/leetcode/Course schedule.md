# Course Schedule

URL: https://leetcode.com/problems/course-schedule/

Categories:
1.[[Kahn's algorithm]] 

Insights:
1. This is a dependency problem, so if we detect a dependency cycle, we can't complete the courses
2. The directedness of the graph's arrows signify 'depends on'.  If node `0` depends on node `1`, the arrow points from `0` to `1`.

Notes:
In practice using `Array.shift()` is pretty inefficient in v8, and **extremely** inefficient for large arrays for which the engine can't optimize the shift and reverts to O(N) behavior.  For some reason Firefox doesn't have this problem.

Solution:
```javascript
var canFinish = function (numCourses, prerequisites) {
    const adj = Array(numCourses).fill(null).map(() => []);
    const inDeg = Array(numCourses).fill(0);
    
    prerequisites.forEach(pq => {
        const [node, wants] = pq;
        
        inDeg[wants]++;
        adj[node].push(wants);
    });
    
    const q = [];
    let opCount = 0;
    
    inDeg.forEach((v, i) => {
        if(v === 0) {
            q.push(i);
        }
    });
    
    while(q.length > 0){
        const dq = q.shift();
        
        adj[dq].forEach(neighbor => {
            --inDeg[neighbor];
            if(inDeg[neighbor] === 0){
                q.push(neighbor);
            }
        });
        
        opCount++;
    }
    
    return opCount === numCourses
}
```