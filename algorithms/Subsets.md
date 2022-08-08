# Subsets

Getting all possible subsets of a group of elements is deceptively simple.  We begin with a solution for the simplest case, which is the empty set (unit)--a subset of all other sets.  In principle, the set of all subsets for the group K, with added element I, is the 
 combination of all subsets of K and the set of subsets formed by adding I to each subset of K.  So for the group of elements `[1]`, all possible subsets are made by combining all the subsets of `[]`, and all the subsets formed by adding `1`  to all the subsets of `[]`.  Thus, `subsets([1]) = [[], [1]]`.

General implementation:
```
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

Note that this could also be done top-down, recursively, since subsets(n) can be programatically derived from subsets(n - 1).

[[Time complexity]] of subset derivation is O(2 ^ (N - 1))