
##   Merge k Sorted Lists

You are given an array of ***```k```*** linked-lists lists, each linked-list is sorted in ascending order.

```Merge all the linked-lists into one sorted linked-list and return it.```


**Example 1**
```bash
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6
```

**Example 2**
```bash
Input: lists = []
Output: []
```

**Example 3**
```bash
Input: lists = [[]]
Output: []
```

### Constraints
- k == lists.length
- 0 <= k <= 104
- 0 <= lists[i].length <= 500
- -104 <= lists[i][j] <= 104
- lists[i] is sorted in ascending order.
- The sum of lists[i].length will not exceed 104.

## Solution

***Using Divide and Conquer***
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
const merge = (l1, l2) => {
    let last, p=l1, q=l2;
    if(l1===null) return l2;
    if(l2===null) return l1;

    if(p.val < q.val) {
        l1=last=p;
        p=p.next;
        l1.next=null;
    } else {
        l1=last=q;
        q=q.next;
        l1.next=null;
    }

    while(p&&q) {
        if(p.val < q.val) {
            last.next=p;
            last=p;
            p=p.next;
            last.next=null;
        } else {
            last.next=q;
            last=q;
            q=q.next;
            last.next=null;
        }
    }

    if(p) last.next = p;
    if(q) last.next = q;
    return l1;
}
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
    let newList = new ListNode();
    for(const list of lists) {
        newList.next = merge(newList.next, list);
    }
    return newList.next;
};
```

***Using Heap***
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(node) {
    this.heap.push(node);
    this.bubbleUp(this.heap.length - 1);
  }

  extractMin() {
    if (this.isEmpty()) return null;

    const minNode = this.heap[0];
    const lastNode = this.heap.pop();

    if (!this.isEmpty()) {
      this.heap[0] = lastNode;
      this.bubbleDown(0);
    }

    return minNode;
  }

  isEmpty() {
    return this.heap.length === 0;
  }

  bubbleUp(index) {
    const parentNodeIndex = Math.floor((index - 1) / 2);
    if (parentNodeIndex >= 0 && this.heap[index].val < this.heap[parentNodeIndex].val) {
      this.swap(index, parentNodeIndex);
      this.bubbleUp(parentNodeIndex);
    }
  }

  bubbleDown(index) {
    const leftChildIndex = 2 * index + 1;
    const rightChildIndex = 2 * index + 2;
    let minIndex = index;

    if (leftChildIndex < this.heap.length && this.heap[leftChildIndex].val < this.heap[minIndex].val) {
      minIndex = leftChildIndex;
    }

    if (rightChildIndex < this.heap.length && this.heap[rightChildIndex].val < this.heap[minIndex].val) {
      minIndex = rightChildIndex;
    }

    if (minIndex !== index) {
      this.swap(index, minIndex);
      this.bubbleDown(minIndex);
    }
  }

  swap(i, j) {
    [this.heap[i], this.heap[j]] = [this.heap[j], this.heap[i]];
  }
}
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
    const minHeap = new MinHeap();

  // Push the head nodes of all lists into the min heap
  for (let list of lists) {
    if (list) {
      minHeap.insert(list);
    }
  }

  let dummy = new ListNode(0);
  let current = dummy;

  // Extract the minimum node from the min heap and append it to the merged list
  while (!minHeap.isEmpty()) {
    const minNode = minHeap.extractMin();
    current.next = minNode;
    current = current.next;

    if (minNode.next) {
      minHeap.insert(minNode.next);
    }
  }

  return dummy.next;
};
```
