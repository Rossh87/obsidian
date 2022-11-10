# Reverse Linked List

URL: https://leetcode.com/problems/reverse-linked-list/description

Categories:
1. [[Linked List]]

Insights:
1. For the recursive solution, the recursive function can always return the head of the new list.  In essence all the recursion does is walk to the bottom of the list and get the head.  Setting `currNode.next.next = currNode` handles the re-ordering.
2. Be sure to unset the forward-ordered links after setting the backward-ordered ones

Notes:

Solution:
```javascript
/**

* Definition for singly-linked list.

* function ListNode(val, next) {

* this.val = (val===undefined ? 0 : val)

* this.next = (next===undefined ? null : next)

* }

*/

/**

* @param {ListNode} head

* @return {ListNode}

*/

// recursive

var reverseList = function(head){

if(head === null || head.next === null) return head;

  

const newHead = reverseList(head.next);

  

head.next.next = head;

  

head.next = null;

  

return newHead;

}

// Extremes: max 5000 nodes

// Emptiness: param node CAN be null

// Sameness: cycles in the list?

// iterative

var reverseList = function(head) {

if(head === null) return null;

  

let oldHead = head.next;

head.next = null;

  

while(oldHead !== null){

const tmp = oldHead.next;

oldHead.next = head;

head = oldHead;

oldHead = tmp;

}

  

return head;

};
```