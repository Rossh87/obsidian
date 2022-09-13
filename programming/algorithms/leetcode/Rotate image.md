# Rotate image

URL: https://leetcode.com/problems/rotate-image/

Categories:
1. 

Insights:
1. Transpose the matrix by swapping row and column for every element, then reverse each row.

Notes:
To keep from swapping elements back into their original position, the lower bound of the inner loop should be set to the current row during transposition step.

Solution:
```javascript
var solve = function (m) {
	const n = m.length;
// transpose
	for(let i = 0; i < n; i++){
		for(let j = i; j < n; j++){
			const t = m[i][j];
			m[i][j] = m[j][i];
			m[j][i] = t;
		}
	};

// reverse each row
	m.forEach(row => row.reverse());

	return m;
}
```