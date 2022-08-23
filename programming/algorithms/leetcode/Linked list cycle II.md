# Linked list cycle II

URL:  https://leetcode.com/problems/linked-list-cycle-ii/

Categories:
1. [[Floyd's algorithm]]

Insights:
1. If `fast`  covers distance at twice the speed of `slow` , eventually either they will land on the same node, or fast will encounter `null`.  
2. If a loop exists, imagine `x` as the distance from start to beginning of cycle, `y` as distance from beginning of cycle to meeting point, and `z` as distance from meeting point  back to beginning of the cycle.
	1. `slow` has moved `x + y`
	2. `fast` has moved `x + y + z + y`, or `2y + x + z`
	3. Since `fast` and `slow` have been incremented the same number of times, and `fast` is moving twice the speed of `slow`,  `2y + x + z = 2(x + y)` 
	4. This expression simplifies to to `x = z`
	5. So, we can move slow back to the start, and increment it along with `fast` on place at a time.  After `z` moves, each will point to the start of cycle, and we have our answer.
	
	

Notes:

Solution:
```javascript
var detectCycle = function(head) {
    if(!head){
        return null;
    }
    
    let fast = head;
    let slow = head;
    
    while(fast != null && fast.next !== null){
        fast = fast.next.next;
        slow = slow.next;
        
        if(fast === slow){
            slow = head;
            
            while(true){
                if(slow === fast){
                    return slow;
                }
                
                slow = slow.next;
                fast = fast.next;
            }
        }
    }
    
    return null;
};
```