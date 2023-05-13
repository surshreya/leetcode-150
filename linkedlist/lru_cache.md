
##   LRU Cache

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache.**

Implement the ***```LRUCache```*** class:

- ```LRUCache(int capacity)``` Initialize the LRU cache with **positive** size ```capacity```.
- ```int get(int key)``` Return the value of the key if the ```key``` exists, otherwise return ```-1```.
- ```void put(int key, int value)``` Update the value of the key if the key exists. Otherwise, add the ```key-value``` pair to the cache. If the number of keys exceeds the capacity from this operation, ```evict the least recently used key```.

The functions get and put must each run in ```O(1)``` average time complexity.
 


 


 




**Example 1**
```bash
Input
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
Output
[null, null, null, 1, null, -1, null, -1, 3, 4]

Explanation
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
```

### Constraints

- ```1 <= capacity <= 3000```
- ```0 <= key <= 104```
- ```0 <= value <= 105```
- ```At most 2 * 105 calls will be made to get and put.```



## Solution

```javascript
class Node {
    constructor(key, val) {
        this.key = key;
        this.val = val;
        this.next = null;
        this.prev = null;
    }
}


class LRUCache {
    /**
        * @param {number} capacity
    */
    constructor(capacity) {
        this.capacity = capacity;
        this.cache = new Map();
        this.head = null;
        this.tail = null;
    }

    /** 
    * @param {number} key
    * @return {number}
    */
    get(key) {
        if(!this.cache.has(key)) return -1;

        const node = this.cache.get(key);
        this.moveToHead(node);
        return node.val; 
    }

    /** 
        * @param {number} key 
        * @param {number} value
        * @return {void}
    */
    put(key, val) {
        if(this.cache.get(key)) {
            //already exists so update
            const node = this.cache.get(key);
            node.val = val;
            this.moveToHead(node);
        } else {
            const node = new Node(key, val);
            this.cache.set(key, node);
            if(this.cache.size > this.capacity) {
                //evict lru item
                const tailKey = this.tail.key;
                this.cache.delete(tailKey);
                this.removeTail();
            }
            this.addToHead(node);
        }
    }

    addToHead(node) {
        if(!this.head) {
            this.head = node;
            this.tail = node;
        } else {
            node.next = this.head;
            this.head.prev = node;
            this.head = node;
        }
    }

    removeNode(node) {
        if (node === this.head) {
            this.head = node.next;
        } else if (node === this.tail) {
            this.tail = node.prev;
        } else {
            node.prev.next = node.next;
            node.next.prev = node.prev;
        }

        node.next = null;
        node.prev = null;
    }

    moveToHead(node) {
        this.removeNode(node);
        this.addToHead(node);
    }

    removeTail() {
        const tail = this.tail;
        this.removeNode(tail);
    }
}


/** 
 * Your LRUCache object will be instantiated and called as such:
 * var obj = new LRUCache(capacity)
 * var param_1 = obj.get(key)
 * obj.put(key,value)
 */
```
