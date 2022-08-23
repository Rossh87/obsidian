# Heap
Sometimes called priority queues, heaps maintain ordered data (max heap, min heap).  They usually expose a method for inserting values and a method for retrieving the highest priority item, which will be the head of the queue.

A heap is technically a set of properties similar to those of a special kind of binary tree rather than any particular data structure, and can be implemented over different structures.  However, an array/list is often convenient.  When a list is used, the key principle  is the the 'child' nodes for any index `i` can be found at `2i + 1` and `2i + 2`.

Surprisingly, implementing a heap from a list has time complexity of O(N) if done correctly.  Iteration should begin at the *end* of the list, and successive elements (working backwards) should be sifted down (rather than up).  

O(N) construction time, and *average* of O(N) insertion time, is due to the distribution of nodes in a binary tree.  50% of all nodes are in the last level (if the tree is full), and about 90% are in the bottom three levels. 

Removing items from the heap is the least efficient operation at O(log N).  This means that some algorithms, like [[Heap sort]] or retrieving the *Kth* smallest/largest item, are bounded by this inefficiency.  For example, to get the smallest K elements from a list, we could construct a min heap from the list (O(N)), then remove K items, giving us O(N + K log N).  A slightly different approach, still bounded by the relative inefficiency of removal, is to add K items to the heap, then go through the remaining items in the list, inserting them into the heap and removing the largest element from the heap, resulting in a min heap of size K.  Because the heap contains a maximum of K elements at any given time, the resulting time complexity is O(N log K).