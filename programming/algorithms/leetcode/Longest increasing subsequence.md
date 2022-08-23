# Longest increasing subsequence

URL: https://leetcode.com/problems/longest-increasing-subsequence/

Categories:
1. [[Dynamic programming]]
2. [[Lower bound, upper bound]]

Insights:
1. The longest subsequence up to a given idx is the longest subsequence up to some previous, smaller-valued element, + 1.  Since we have a base case of a single element always constituting a subsequence of 1, we can build up a dynamic programming array and for every idx `i`, we search from 0  to `i - 1` for an element smaller than nums\[i\],  and check the subsequence length up to that smaller element.  Because we have to check from 0 to `i` for all indices `i`, time complexity is O(N^2).
2. O(N log N) approach depends on the fact that the increasing sequence array is sorted.  Because of this, we can update it with subsequent elements from the list, using O(log N) bisection to find the appropriate index to update.  In the end, the length of the increasing sequence array is the answer.

Notes:
Consider this list:
```javascript
[1,100, 2,3,4,5]
```
A naive approach will fail, because 100 will become the tail of the subsequence, and the rest will be skipped even though they are sequential.  To fix this problem, we want the tail of the subsequence to update to the smallest encountered value that maintains the subsequence in sorted order.

Solution:
```javascript
const lowerBound = (arr, target) => {
	let l = 0;
// Remember that this function can return arr.length
// if target is larger than all existing elements.
let h = arr.length;

	while(l < h){
		if(arr[mid] >= target){
			h = mid;	
		} else {
			l = mid + 1;	
		}
	}

	return l;
}

const lengthOfLIS = (nums) => {
	const res = [];

	for(let num of nums){
		if(res.length === 0 || res[res.length - 1] < num){
			res.push(num);	
		} else {
			res[lowerBound(res, num)] = num;	
		}
	}

	return res.length;
}
```