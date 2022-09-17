# Alien dictionary

URL: https://leetcode.com/problems/alien-dictionary/

Categories:
1. [[Kahn's algorithm]]
2. [[Topological sorting]]

Insights:
1. The only way to get useful information from the dictionary is to compare the *first differing character* of successive words
2. Each piece of information can be represented as a directed edge from one letter to another
3. If there is a cycle in the resulting graph, the dictionary is invalid

Notes:
Once you know the approach to use, the hardest part of this problem is the bookkeeping.  Be very careful to check for all the cases that render the dictionary invalid, esp. in the 'first differing character' part.

Solution:
```javascript
// DFS/postorder traversal
var alienOrder = function(words){
    const nodes = new Map();
    
    words.forEach(w => {
        for(let char of w){
            if(nodes.get(char) === undefined){
                nodes.set(char, new Set());
            }
        }
    });
    
    for(let i = 0; i < words.length - 1; i++){
        const word1 = words[i]
        const word2 = words[i + 1];
        
        let ptr = 0;
        let char1 = word1[ptr];
        let char2 = word2[ptr];
        while(char1 !== undefined && char2 !== undefined && char1 === char2){
            ptr++;
            char1 = word1[ptr];
            char2 = word2[ptr];
        }
        
        if(char2 === undefined && char1 === undefined) continue;
        
//         if second word is longer than first and first is prefix of second,
//         we can't extract any info from this pair
        if(char1 === undefined) continue;
        
        if(char2 === undefined) return "";
        
        nodes.get(char1).add(char2);
    }
    
    let result = "";
//     if visited[char] === true, it means we've re-encountered a node that's in the 
//     current traversal path--i.e., we've found a cycle, so the DAG is invalid.  If it's
//     false, the node was processed as part of a previous path, so we just return--no need
//     to deal with the node or any of its children.
    const visited = new Map();
    
    const dfs = (char) => {
        if(visited.get(char) !== undefined){
            return visited.get(char);
        }
        
//         we're currently processing this node, so mark it
//         in current path
        visited.set(char, true);
        
        const children = nodes.get(char);
        
        for(let child of children){
            if(dfs(child)) return "";
        }
        
        result += char;
        
        visited.set(char, false);
        return false;
    }
    
    for(let char of nodes.keys()){
        if(dfs(char)){
            return "";
        };
    }
    
    return result.split('').reverse().join('');
}
// Kahn's algo, BFS
var alienOrder = function(words) {
    const graph = new Map();
    
    words.forEach(w => {
        for(let char of w){
            if(graph.get(char) === undefined){
                graph.set(char, new Set());
            }
        }
    });
    
//     Notice we stop loop 1 before end, since we're taking words in pairs
    for(let i = 0; i < words.length - 1; i++){
        const word1 = words[i];
        const word2 = words[i + 1];
        
        let p1 = 0; 
        let p2 = 0;
        
        while(word1[p1] === word2[p2] && word1[p1] !== undefined && word2[p2] !== undefined){
            p1++;
            p2++;
        }
        
        if(word1[p1] === undefined || word2[p2] === undefined){
            if(word1[p1] !== undefined && word2[p2] === undefined){
                return "";
            }
            
            continue;
        }
        
        const edgeList = graph.get(word2[p2]);
        edgeList.add(word1[p1]);
    }
    
    
    
    let processedCount = 0;
    
    const q = [];
    
    const entries = Array.from(graph.entries());
    
    entries.forEach((entry) => {
        const [char, incoming] = entry;
        
        if(incoming.size === 0){
            q.push(entry);
        }
    })
    
    let result = "";
    
    while(q.length > 0){
        const currEntry = q.shift();
        
        processedCount++;
        
        result += currEntry[0];
        
        entries.forEach((graphEntry) => {
            const incoming = graphEntry[1];
            const prevSize = incoming.size;
            
            if(prevSize === 0) return;
            
            incoming.delete(currEntry[0]);
            
            if(incoming.size === 0 && prevSize === 1){
                q.push(graphEntry);
            }
        });
    }
    
    if(processedCount === members.size) return result;

    return "";
};
```