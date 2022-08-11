# Word break

URL: https://leetcode.com/problems/word-break/

Categories:
1. [[Dynamic programming]]
2. [[Backtracking]]

Insights:
1. A backtracking approach yields correct result, but has time complexity on the order of N ^ N.  If we graph out the decision tree for a simple string, we'll see that many of the branches test the same inputs.  This is a sign that a dynamic programming approach could save some time.
2. Dynamic programming can work because a  given substring is `true` if it is true, and the substring to the right or left of it is true, depending on which direction we're processing the string in.  We need to store the results of checking  certain substrings, and we can do this *either* by storing substrings with a boolean (e.g. in a map), *or* by storing whether the string up to a certain index is viable

Notes:

Solution:
```javascript
// bottom-up iterative
var wordBreak = function (s, wordDict){
//     dict to map for efficient retrieval
    const dict = new Set(wordDict);
//     store whether substring up to certain idx is valid
    const idx = new Map();
    
    for(let i = 0; i < s.length; i++){
//         try to 'slot' each dict word in
        for(let word of dict){
            const wl = word.length - 1;
            const wordStart = i - wl;
            
            if(wordStart < 0){
                continue;
            }
            
            if(s.slice(wordStart, i + 1) === word && (idx.get(wordStart - 1) === true || wordStart === 0)){
                if(i === s.length - 1){
                    return true;
                }
                
                idx.set(i, true);
                break;
            }
        }
        
        if(idx.get(i) === undefined){
            idx.set(i, false);
        }
    }
    
    return false;
}

// top-down recursive
var wordBreak = function (s, wordDict){
    const dict = new Set(wordDict);
    const idx = new Map();
    
    const search = (ss) => {
        if(dict.has(ss)) return true;
        
        if(idx.get(ss) !== undefined) return idx.get(ss);
        
        for(let i = 0; i < ss.length; i++){
            const candidate = ss.slice(0, i + 1);
            
            if(dict.has(candidate) && search(ss.slice(i + 1))){
                idx.set(ss, true);
                return true;
            } 
        }
        
        idx.set(ss, false);
        return false;
    }
    
    return search(s);
}
}
```