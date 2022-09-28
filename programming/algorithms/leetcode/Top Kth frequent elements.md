# Top Kth frequent elements

URL: https://leetcode.com/problems/top-k-frequent-elements/

Categories:
1. [[Heap]]
2. [[Quicksort]] (quickselect)

Insights:
1. No element can occur more than `nums.length` times, so we can use the indices of an array of size `nums.length + 1` to store the number of times any given element occurs in the original array.
2. Better alternative is arguably to use quickselect; use the number of occurences to figure out the sorted order.  When sorted position is >= k, we can be done: just slice `k` elements off the front of the array.

Notes:
Bucket-based solution (see insight 1 above) is O(N), but wastes a lot of memory on empty array allocation if the input array contains only a few unique members that occur many times.  Construction of the result also contains many wasted iterations in this case (we end up looping over many empty arrays).  With a relatively even distribution of occurences over the array's distinct elements, a minor optimization can be had by tracking the maximum number of occurences of any element on the initial iteration, and only initializing the 'sorting' array to that length.

Heap-based solution is O(N + K log N): N to construct the heap, and then K removals, each at a cost of log N.  The worst-case for this approach is an array of all-unique elements, and K = nums.length.  That gives us N + N log N, or 2N log N, which is O(N log N), which is technically ruled out by the question requirements.  

Solution:
```javascript
// O(N) time and memory, but hidden constant memory use is high
// in many cases compared to e.g. a heap-based approach
var topKFrequent = function(nums, k) {
    const idx = new Map()
    
    for(let num of nums){
        const ext = idx.get(num) ?? 0
        idx.set( num, ext + 1);
    }
    
    const buckets = Array(nums.length + 1).fill(null).map(() => []);
    
    Array.from(idx.entries()).forEach(([num, occurences]) => {
        buckets[occurences].push(num);
    })
    
    const result = [];
   
    for(let i = buckets.length - 1; i >= 0; i--){
        if(result.length === k) break;
        
        if(buckets[i].length > 0){
            buckets[i].forEach(el => result.push(el));
        }
    }
    
    return result;
};

// quickselect approach: average O(log N)
const qs = (l, r, arr, occ, k) => {
    const pivot = r;
    const pivotVal = occ.get(arr[pivot]);
    let insertPos = l - 1;
    for(let i = l; i < pivot; i++){
        if(occ.get(arr[i]) > pivotVal){
            insertPos++;
            swap(i, insertPos, arr);
        }
    }
    
    insertPos++;
    swap(pivot, insertPos, arr);
        
    if(insertPos === k - 1) return;
    
    if(insertPos < k - 1) {
        return qs(insertPos + 1, r, arr, occ, k)
    }
    
    return qs(l, insertPos - 1, arr, occ, k);
}

var topKFrequent = function(nums, k){
    const occurences = nums.reduce((acc, num) =>{
        const count = acc.get(num) ?? 0;
        
        acc.set(num, count + 1);
        
        return acc;
    } , new Map());
     
    console.log(occurences)
    nums = Array.from(occurences.keys());
    
    qs(0, nums.length - 1, nums, occurences, k);
    
    return nums.slice(0, k);
}
```