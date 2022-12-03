# task-scheduler

URL: https://leetcode.com/problems/task-scheduler/description/

Categories:
1. [[Greedy]]

Insights:
1. The largest number of idle slots is `(mostFrequentTask - 1) * cooldown`
2. For every task of less or equal frequency to `maxFreqTask`, we can use a number of idle slots equal to `min(maxFreq - 1, currentFreq)`.  We need the minimum in case `currentFreq` is the **same** as  `maxFreq`.
3. Just never let idle slot go less than 0.

Notes:

Solution:
/**

* @param {character[]} tasks

* @param {number} n

* @return {number}

*/

// extremes: n = 0

// emptiness:

// sameness: all same task

// count occurences of each task (O(N))

// while occurences.size > 0

var leastInterval = function(tasks, n) {

const offset = 'A'.charCodeAt(0);

const occurences = Array(26).fill(0);

  

tasks.forEach(t => {

const code = t.charCodeAt(0);

const pos = code - offset;

occurences[pos] += 1;

})

  

occurences.sort((a, b) => b - a);

  

const maxFreq = occurences[0];

let maxIdle = (maxFreq - 1) * n;

  

for(let i = 1; i < occurences.length && maxIdle > 0; i++){

maxIdle -= Math.min(occurences[i], maxFreq - 1);

}

  
// this check is very important!!
maxIdle = Math.max(0, maxIdle)

return tasks.length + maxIdle;

};
```