# Subsets

The number of possible subsets that can be formed from a set of size `N` is 2 ^ `N`.  Intuitively, for any given subset, each member of the superset can either be *in* or *out* (i.e. 2 possibilities), giving a formula of `2 * 2 * ...`.

Iterative appreach: begin with a solution for the simplest case, which is the empty set (unit)--a subset of all other sets.  In principle, the set of all subsets for the group K, with added element I, is the 
 combination of all subsets of K and the set of subsets formed by adding I to each subset of K.  So for the group of elements `[1]`, all possible subsets are made by combining all the subsets of `[]`, and all the subsets formed by adding `1`  to all the subsets of `[]`.  Thus, `subsets([1]) = [[], [1]]`.

Iterative implementation:
```javascript
// Given a list of unique elements 'nums'
var subsets = function(nums) {
    const result = [[]];
    
    if(nums.length === 0){
        return result;
    }
 
    for(let i = 0; i < nums.length; i++){
	    //need to capture length here, BEFORE we 
	    //start modifying result array
        const n = result.length;
        for(let j = 0; j < n; j++){
            result.push([...result[j], nums[i]])
        }
    }
    
    return result;
}
```

The recursive implementation of this problem is useful for any problem where we need to try all combinations of something.  In each recursive layer, we branch once while *taking* the current element, and again without taking it.  Note that below, the sets are **true** `sets`, in the since that all elements are unique within each set, but the [[Backtracking]] approach below does not require that constraint to be useful.  Combine with [[Dynamic programming]] to prune branches of the search tree and remove needless recursion whenever possible, as this approach runs in exponential time.

```javascript
var subsets = function(nums) {
    const result = [];
    
    const bt = (idx, partial) => {
        if(idx === nums.length){
            result.push(partial.slice());
            return;
        }
        
        partial.push(nums[idx]);
        bt(idx+1, partial);
        partial.pop();
        bt(idx+1, partial);
    }
    
    bt(0, []);
    
    return result;
}
```

