
##  Reverse Linked List II

Given the head of a singly linked list and two integers ```left``` and ```right``` where ```left <= right```, reverse the nodes of the list from position left to position right, and return ```the reversed list.```
![rev2ex2](https://github.com/surshreya/leetcode-150/assets/118065908/51266d58-fc99-412f-a61f-3f31d9f7697b)

**Example 1**
```bash
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```

**Example 2**
```bash
Input: head = [5], left = 1, right = 1
Output: [5]
```

### Constraints
- The number of nodes in the list is n.
- 1 <= n <= 500
- 500 <= Node.val <= 500
- 1 <= left <= right <= n
 
## Solution

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} left
 * @param {number} right
 * @return {ListNode}
 */
var reverseBetween = function(head, left, right) {
    let cur = head;
    let prev = null;

    let i;
    for(i=1;i<left;i++) {
        prev = cur;
        cur = cur.next;
    }
    
    let subTail = cur;
    let subHead = null;

    while(i<=right) {
        let node = cur.next;
        cur.next = subHead;
        subHead = cur;
        cur = node;
        i++;
    }

    if(prev != null)
        prev.next = subHead;
    else
        head = subHead;
    subTail.next = cur;

    return head;
};
```
