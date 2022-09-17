# Min-stack

URL: https://leetcode.com/problems/min-stack/

Categories:
1. 

Insights:
1. Simplest way is to use a single array, and with each pushed element store the current min as part of a tuple
2. To conserve a little space, use a second list to track the min.  The final element of the list represents the minimum at any given time.  The elements on the minimum-tracking list are tuples: they hold the value and the number of occurences of the value.  If an element is pushed that is equal to current min, update number of occurences of that min.  If element is pushed that is less-than current min, push a new element to min-tracking list with 1 occurence.  Reverse this logic when popping.

Notes:

Solution:
```javascript
var MinStack = function() {
    this.mins = [];
    this.stack = [];
};

/** 
 * @param {number} val
 * @return {void}
 */
// minimums element has shape [value, occurences]
MinStack.prototype.push = function(val) {
    this.stack.push(val);

    if(this.stack.length === 1){
        this.mins.push([val, 1]);
        return;
    }
    
    const minTail = this.mins[this.mins.length  - 1];
    
    if(val < minTail[0]){
        this.mins.push([val, 1]);
        return;
    }
    
    if(val === minTail[0]){
        minTail[1]++;
    }
    
    return;
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function() {
    const popped = this.stack.pop();
    
    const minTail = this.mins[this.mins.length - 1];
    
    if(popped === minTail[0]){
        if(minTail[1] === 1){
            this.mins.pop();
        } else {
            minTail[1]--;
        }
    }
    
    return popped;
};

/**
 * @return {number}
 */
MinStack.prototype.top = function() {
    return this.stack[this.stack.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function() {
    const minTail = this.mins[this.mins.length - 1];
    
    return minTail[0];
};

```