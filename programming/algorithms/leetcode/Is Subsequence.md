URL: https://leetcode.com/problems/is-subsequence/?envType=study-plan&id=level-1

Categories:
1. [[Iteration]]

Insights:
1. We can parse the character indices of superstring `t` into a map so that we can lookup in O(1) rather than re-iterating if we are going to run the algorithm many times

Notes:

Solution:
```javascript
var isSubsequence = function(s, t) {

const charPositions = new Map();

  

for(let i = 0; i < t.length; i++){

const char = t[i];

  

const existing = charPositions.get(char);

  

if(existing === undefined){

charPositions.set(char, [i]);

continue;

}

  

existing.push(i);

}

  

let parentPos = -1;

  

for(let i = 0; i < s.length; i++){

const subChar = s[i];

  

const positions = charPositions.get(subChar);

  

if(positions === undefined) return false;

  

let found = false;

for(let j = 0; j < positions.length; j++){

const pos = positions[j];

  

if(pos > parentPos){

parentPos = pos;

found = true;

break;

}

}

  

if(!found) return false;

}

  

return true;

};
```