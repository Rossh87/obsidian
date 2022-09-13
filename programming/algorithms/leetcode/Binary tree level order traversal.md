# Binary tree level order traversal

URL: https://leetcode.com/problems/binary-tree-level-order-traversal/submissions/

Categories:
1. [[Breadth-first search]]

Insights:
1. Using a first-in-first-out queue makes the traversal very easy to visualize

Notes:
A linked list is a simple way to homeroll a FIFO queue that adds/removes in constant time, since `Array.prototype.shift` performs badly with long lists

We can get away with using a single queue by tracking the number of elements in the queue at the end of each level and only `shift`ing off that many nodes, rather than instantiating a second queue.

Solution:
```javascript
class QNode {
    constructor(v){
        this.val = v;
        this.next = null;
    }
}

class Q {
    constructor(){
        this.head = null
        this.tail = null;
        this.len = 0;
    }
    
    append(v){
        const n = new QNode(v);
        
        if(this.len === 0){
            this.head = n;
            this.tail = n;
            this.len++;

            return;
        }
        this.len++;

        this.tail.next = n;
        this.tail = n;
    }
    
    shift(){
        if(this.head === null) return null;
        
        const n = this.head;
        this.head = n.next;
        
        if(this.head === null){
            this.tail = null;
        }
        
        this.len--;
        return n;
    }
}

var levelOrder = function(root) {
    const result = [];
    
    if(root === null) return result;
    
    let q = new Q()
    
    q.append(root);
    
    while(q.len > 0){
        const out = [];
        let prevRow = q.len;
        while(prevRow > 0){
            const n = q.shift().val;
            
            out.push(n.val);
            
            if(n.left !== null){
                q.append(n.left);
            }
            
            if(n.right !== null){
                q.append(n.right);
            }
            
            prevRow--;
        }
        
        result.push(out);
    }
    
    return result;
};
```