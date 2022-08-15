# Tortoise and hare

Useful in linked lists for finding the midpoint of the list.  General idea is to start 2 pointers at list head, then increment 1 twice as fast as the other for as long as possible.  When we can no longer increment fast, slow will be at the middle node. 
```javascript
let slow = listHead;
let fast = listHead;

while(fast !== null && fast.next !== null){
	slow = slow.next;
	fast = fast.next.next;
}

const midNode = slow;
```

Note that for [[Binary search]] of linked list, a slight modification to the above is needed.  For an even number of nodes, this approach rounds *up*; i.e., for a list of 4 members, it will give us node 3.  To properly binary search, node 3 should be the beginning of the right-hand search, but we also need to break the link between node 2 and three, and we have no way to go back.  To get the *rounded down*  midpoint (i.e. the *last* element of the left-hand search), either set a third pointer that lags 1 behind `slow`, or stop the `while` loop 1 tick sooner by checking `fast.next.next !== null`.
```javascript
let slow = listHead;
let fast = listHead;

while(fast.next !== null && fast.next.next !== null){
	slow = slow.next;
	fast = fast.next.next;
}
```