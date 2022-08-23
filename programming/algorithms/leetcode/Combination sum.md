# Combination sum

URL: https://leetcode.com/problems/combination-sum/

Categories:
1. [[Backtracking]]

Insights:
1. Handle 'branching' of recursive backtracking inside a 'for' loop
2. Search space will be an *N*-ary tree where *N* is the number of children of each node
3. Be careful about array mutation

Notes:
This is a kind of backtracking problem, where at each array 'stub', we can either add another of the candidate we're currently iterating on, OR we can move on to the next candidate.  Since we can construct a solution incrementally, and we can verify whether or not partial solutions are still viable, this problem is susceptible to backtracking.

The tricky bit is in the looping: we have to try building a solution starting with each candidate position, and within each start we have to try adding all 'downstream' candidates.

Time complexity is (I think) O(N!), where N is the length of 'candidates'.  We loop over candidate positions from 0 to end, and within each loop run an inner loop from (pos) to end.  Because each tick of the outer loop eliminates 1 candidate element, we end up with something like (ln \* ln - 1 \* ln -2 ... 0).  There is a coefficient for each loop that equals approx (target / candidates\[loopPosition\])

Solution:
```javascript
var solve = function () {
	const result = [];
    
    const list = [];
    
//     write recursive fn that takes a starting idx and the amount remaining until 
//     target is reached
    const backtrack = (startIdx, remaining) => {
        if(remaining === 0){
            result.push(list.slice());
            return;
        }
        
        if(remaining < 0){
            return;
        }
        
        for(let i = startIdx; i < candidates.length; i++) {
            list.push(candidates[i]);
            backtrack(i, remaining - candidates[i]);
            list.pop();
        }
    }
    
    backtrack(0, target);
    
    return result;
}
```