# Generate parentheses

URL: https://leetcode.com/problems/generate-parentheses/

Categories:
1. [[Backtracking]]

Insights:
1. By tracking the number of open **and** closed parentheses remaining, we can predict whether a partial candidate will be valid or not without needing to walk it.

Notes:
It is also possible to solve this with top-down recursion and dynamic programming, i.e. recursing from `f(n)` through `f(n - 1)` down to `f(1)`, which is a known quantity `()`.  The forumula is complicated, however; the recursion tree is much easier to understand with the following approach.

Solution:
```javascript
var generateParenthesis = function(n) {
    const result = [];
    
    const cand = [];
    
    const bt = (ps, open, close) => {
        if(open === 0 && close === 0){
            result.push(ps.join(""));
            return;
        }
        
        if(open === close){
            ps.push("(");
            bt(ps, open - 1, close);
            ps.pop();
            return;
        }
        
        if(open === 0){
            ps.push(")");
            bt(ps, open, close - 1);
            ps.pop();
            return;
        }
        
        ps.push("(");
        bt(ps, open - 1, close);
        ps.pop();
        
        ps.push(")");
        bt(ps, open, close - 1);
        ps.pop();
    }
    
    bt(cand, n, n);
    
    return result;
};
```