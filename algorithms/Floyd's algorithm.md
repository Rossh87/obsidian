# Floyd's algorithm

Used to detect cycles in linked lists.

Works by running a fast pointer at some fixed speed greater than a slow pointer.  If there is a cycle, the fast will necessarily overtake the slow.  From there, find various points in the cycle by the following logic:

If a loop exists, imagine `x` as the distance from start to beginning of cycle, `y` as distance from beginning of cycle to meeting point, and `z` as distance from meeting point  back to beginning of the cycle.
	1. `slow` has moved `x + y`
	2. `fast` has moved `x + y + z + y`, or `2y + x + z`
	3. Since `fast` and `slow` have been incremented the same number of times, and `fast` is moving twice the speed of `slow`,  `2y + x + z = 2(x + y)` 
	4. This expression simplifies to to `x = z`
	5. So, we can move slow back to the start, and increment it along with `fast` on place at a time.  After `z` moves, each will point to the start of cycle.