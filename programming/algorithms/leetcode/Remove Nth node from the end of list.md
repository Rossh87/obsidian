# Remove Nth node from the end of list

URL: https://leetcode.com/problems/remove-nth-node-from-end-of-list/

Categories:
1. 

Insights:
1. Can be done in O(N) time and constant memory with two pointers, spaced `n` nodes apart.  Create the spacing, then walk each node until the farther node reaches the end of the list.  At this point the slower node should be 1 before the node to be removed, so do the appropriate splice.

Notes:
Care should be taken for case where `n` = 1 and `n` = (nodeCount)

Solution:
```javascript
var removeNthFromEnd = function(head, n) {
    let slow = head;
    let fast = head;
    
    while(n > 0){
        fast = fast.next;
        n--;
    }
    
    if(fast === null){
//         n was equal to number of nodes--remove head of list and return.
//         note this also covers case of only 1 node in list
        return head.next;
    }
    
    while(fast.next !== null){
        fast = fast.next;
        slow = slow.next;
    }
    
    slow.next = slow.next.next;
    
    return head;
};
```