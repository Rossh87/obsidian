# Palindrome Linked List

URL: https://leetcode.com/problems/palindrome-linked-list/description/?envType=study-plan&id=level-2

Categories:
1. [[Linked List]]
2. [[Tortoise and hare]]

Insights:
1. Easiest way is O(N) time and memory: just copy the list's values into an array, then use 2-pointer technique to check for palindrome.
2. To get O(1) memory, find the end of the first half using tortoise and hare, reverse the second half of the list, check for palindrome, then fix the list.

Notes:
Be careful to stop the slow pointer at the *end* of the first half, not the beginning of the second!

When running slow/fast pointers, be careful to check if `fast.next` is `null` before checking `fast.next.next`!

Solution:
```javascript
/**

* @param {ListNode} head

* @return {boolean}

*/

const reverseList = (head) => {

let prev = null;

let current = head;

  

while(current !== null) {

const tmp = current.next;

current.next = prev;

prev = current;

current = tmp;

}

  

return prev;

}

  

var isPalindrome = function(head) {

if(head.next === null) return true;

  

let slow = head;

let fast = head;

  

while(fast.next !== null && fast.next.next !== null){

slow = slow.next;

fast = fast.next.next;

}

  

const firstHalfEnd = slow;

const secondHalfStart = reverseList(firstHalfEnd.next)

firstHalfEnd.next = secondHalfStart;

  

let p1 = head;

let p2 = secondHalfStart;

  

while(p2 !== null){

if(p1.val !== p2.val) return false;

p1 = p1.next;

p2 = p2.next;

}

  

// repair the list

firstHalfEnd.next = reverseList(secondHalfStart);

  

return true;

};
```