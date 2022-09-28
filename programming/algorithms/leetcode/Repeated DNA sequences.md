# Repeated DNA sequences

URL: https://leetcode.com/problems/repeated-dna-sequences/

Categories:
1. [[Rolling hash]]

Insights:
1. (see above)

Notes:
Note we need to track both `seen` strings and `result` strings; `Set` works well for this.

In general, we should always be able to use the sliding window technique in 'duplicate strings' problems like this, which we can complete in `O(1)` time.  The tricky bit consists of maximizing the efficiency of the comparison we make each time the window moves.  However, in this particular problem, even the worst comparison approach where we slice the substring each time and compare is technically still `O(N)` time, since the number of comparisons per window move is a constant 10.

Solution:
```javascript
var findRepeatedDnaSequences = function(s) {
    if(s.length < 10) return [];
    
    const seen = new Set();
    
    const dupes = new Set();
    
    const values = {
        A:0,
        C:1,
        G:2,
        T: 3
    };
    
    const base = 4;
    
    let h = 0;
    
    for(let i = 0; i < s.length; i++){
        const char = s[i];
        
//         populate initial window hash
        if(i < 10){
            h = h * base + values[char];
            continue;
        }
        
        if(seen.has(h)){
            dupes.add(s.slice(i - 10, i));
        }
        
        seen.add(h);
        
        h = h * base - (values[s[i - 10]] * Math.pow(base, 10)) + values[char];
    }
    
//     run dupe check once more here
    if(seen.has(h)){
        dupes.add(s.slice(s.length - 10, s.length));
    }
    
    return Array.from(dupes);
};
```