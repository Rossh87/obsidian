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

Solution:
```javascript
var solve = function () {

}
```