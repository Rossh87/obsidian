# Number of connected components in undirected graph

URL: https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/

Categories:
1. [[Union find]]
2. [[Depth-first search]]

Insights:
1. Union find approach is possible because adding an edge between 2 vertices is conceptually equivalent to creating a union set of each element, for the purposes of this problem.
2. Time/space complexity for union find is pretty complicated, but time comes out to something like `O(E * log V)`, where `E` is the number of edges and `V` is the number of vertices, since average number of levels in tree with `V` nodes will be `log V` and we walk each edge calling the `find` function.

Notes:
DFS is probably simpler to think about, and to calculate time complexity
Solution:
```javascript
// union find:
// 1. create parentOf list
// 2. map edges and union the vertices of each edge
// 3. walk vertices and call find(vtx) on each one.  Track the
// parents we see; every time we find a new parent, we have a unique subset
// Needed: fn union(x, y), fn parentFind(x, y), var seenParent = new Set()

const findParent = (parentList) => (x) => {
    if(parentList[x] === x) return x;
    
    return findParent(parentList)(parentList[x]);
}

const union = (parentList) => ([x, y]) => {
    const fp = findParent(parentList);
    
    const p1 = fp(x);
    const p2 = fp(y);
    
//     vertices are already part of same subset
    if(p1 === p2) return 0;
    
    parentList[p1] = p2;
    return 1;
}

var countComponents = function(n, edges) {
    let components = n;
    
    const parentList = Array(n).fill(-1).map((_, i) => i);
    
    edges.forEach((edge) => components -= union(parentList)(edge));
    
    return components;
};

// DFS:
// 1. build adjacency list
// 2.init array to track visited vertices
// 3. call dfs on 0 = (n - 1)
// 4. dfs(vtx): if visited[vtx] === true, return
// else, visited[vtx] = true & dfs(all vertices in adjacent[vtx])
// Time: O(E + V): adjacency list time is based on number of edges, 
// and DFS time is based on number of vertices
// Space: O(E + V): adjacency list scales with number of edges, and 
// keeping track of 'seen' vertices take O(V).  Also DFS function stack takes
// O(V) (worst case V calls if there is only a single component in the graph)
var countComponents = function(n, edges){
    const visited = Array(n).fill(false);
    
    const adjacent = Array(n).fill(null).map(() => []);
    
    let components = 0;
    
    edges.forEach(([x, y]) => {
        adjacent[x].push(y);
        adjacent[y].push(x);
    });
    
    const dfs = (vtx) => {
        if(visited[vtx]) return;
                
        visited[vtx] = true;
        
        adjacent[vtx].forEach(child => dfs(child));
    };
    
    adjacent.forEach((neighbors, i) => {
        if(visited[i]) return;
        
        components++;
        
        dfs(i);
    });
    
    return components;
}
```