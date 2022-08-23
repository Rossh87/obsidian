# LRU cache
A least-recently-used cache is a common key-value style cache that also appears in data structure interview questions.  The cache contains a fixed number of elements. New elements can be inserted until the capacity is reached; after that, the element that was 'touched' the longest time ago is evicted before any new elements are added.

A common approach to implementing this style of cache is to use a hashmap combined with a doubly-linked list to maintain O(1) lookup and insertion performance.  The hashmap contains references to nodes in the list, and the list can be updated based on node references recovered from the hashmap.  The list itself need only maintain a reference to its first and last elements, since the nodes themselves contain information needed to update their neighbors when appropriate.

Care must be taken when implementing the 'insert' logic for the cache: 'insert' instructions for keys that are already in the cache should be treated as update requests that also constitute a 'touch' of the relevant node.

Below is an example JS implementation
```javascript
class ListNode {
    constructor(k, v, older, newer){
        this.key = k;
        this.value = v;
        this.older = older;
        this.newer = newer;
    }
}

class Dll {
    constructor(){
//         head = oldest, tail = newest
        this.head = null;
        this.tail = null;
        this.size = 0;
    }
    
    moveToTail(node){
        //         3 possibilities: node is oldest, node is newest, or node is in the middle
//         node is already newest
        if(node === this.tail) return;
        
//         node is oldest
        if(node.older === null){
            this.head = node.newer;
            this.head.older = null;
            this.tail.newer = node;
            node.older = this.tail;
            node.newer = null;
            this.tail = node;
            return;
        }
        
//         node is in middle
        node.older.newer = node.newer;
        node.newer.older = node.older;
        this.tail.newer = node;
        node.older = this.tail;
        node.newer = null;
        this.tail = node;
        return;
    }
    
    update(node, v){
        node.value = v;
        return;
    }
    
    append(node){
        this.size++;
        
        if(this.head === null){
            this.head = node;
            this.tail = node;
        } else {
            this.tail.newer = node;
            node.older =this.tail;
            this.tail = node;
        }
        
        return;
    }
    
//     remove oldest from list;
    shift(){
        this.size--;
        
        if(this.tail === this.head){
            this.head = null;
            this.tail = null;
            return;
        }
        
        this.head = this.head.newer;
        this.head.older = null;
        return;
    }
}

```