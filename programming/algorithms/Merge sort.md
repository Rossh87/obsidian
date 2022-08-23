# Merge sort

Sorting algorithm with O(N log N) time complexity and varying memory requirements depending on the structure being sorted.

It is particularly useful for linked lists, as it requires no new memory allocation for the list structure.  See [[Tortoise and hare]] for finding the midpoint of a linked list.

The main idea is that two sorted sublists can be **merged** by looking at the head of each list, appending whichever element is smallest to a new list, and continuing until both sublists are empty and all their members have been added to the new list.

To get the first sorted sublists, we take two lists, each with one item apiece (which is necessarily sorted).

To do this recursively, proceed similarly to a [[Binary search]]: find the midpoint of the list, split the list there, and call the recursive function on each sublist to get a sorted sublist from each half.  This yields a [[Depth-first search]] effect: the left sublist recurses until only a single element remains, which is the recursive function's boundary condition.  The parent of the deepest call then receives a single element from each of its child calls, merges the elements, and returns.  This continues until the first function call receives the sorted left and right halves of the original list, which it merges and returns.

Iterative merge sort is conceptually simple, but implementation is tricky.  Main driver is an outer loop that stores the length of a given subarray, starting with 1 and doubling each incrementation.  Because, a subarray of length 1 is inherently sorted, we can then run an inner loop that operates on (sublength * 2) elements at a time, merges them, and updates the array in-place.  Now each subarray of length 2 in the original array is sorted, and we can increment subarray length to 2.  Continue as long as sublength is less than length of the original array.

Great care must be taken with the merge function, because the length of the input array will often not be a power of 2.  When this is the case, `merge` will end up being called with a `start` and `end` that does not contain enough members to form two complete subarrays.  When this is the case, `merge` should simple return all of the members it receives in the order it receives them, since they will already have been sorted as part of smaller subarrays.

```javascript
const iterMergeSort = (arr) => {

const ln = arr.length;

if (ln === 1) return arr;

for (let subLength = 1; subLength < ln; subLength *= 2) {
	for (let start = 0; start < ln - 1; start += subLength * 2) {
// NOTE taking minimums here
		const mid = Math.min(start + subLength - 1, ln - 1);

		const end = Math.min(start + subLength * 2 - 1, ln - 1);

		merge(arr, start, mid, end);
	}
}

  

function merge(arr, start, mid, end) {

	const sorted = [];
	
	let lp = start;
	
	let rp = mid + 1;
	
	let lItemCount = mid - start + 1;

// If mid and end are the same due to taking minimums above,
// there will be no items in the right subarray, and merge will
// simply return the already-sorted items it has received.
let rItemCount = end - mid;
	
	while (lItemCount > 0 || rItemCount > 0) {
	
	if (lItemCount > 0 && rItemCount > 0) {
	
		if (arr[lp] < arr[rp]) {
		
			sorted.push(arr[lp]);
			
			lp++;
			
			lItemCount--;
			
			continue;
		
		}
	
		sorted.push(arr[rp]);
		
		rp++;
		
		rItemCount--;
		
		} else if (lItemCount > 0) {
		
			while (lItemCount > 0) {
			
			sorted.push(arr[lp]);
			
			lp++;
			
			lItemCount--;
			
			}
		
		} else {
		
			while (rItemCount > 0) {
			
			sorted.push(arr[rp]);
			
			rp++;
			
			rItemCount--;
			
			}
		
		}

}

  

// console.log(sorted);

let sortedPos = 0;

  

for (let i = start; i <= end; i++) {

arr[i] = sorted[sortedPos];

sortedPos++;

}

}

  

return arr;

};
```