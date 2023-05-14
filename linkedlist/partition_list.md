
##  Partition List

Given the ```head``` of a linked list and a value ```x```, partition it such that all nodes **less than** x come before nodes **greater than or equal** to x.

You should **preserve** the original relative order of the nodes in each of the two partitions.
![partition](https://github.com/surshreya/leetcode-150/assets/118065908/5ed3699b-deee-4e6c-8361-d0327475f4c5)

**Example 1**
```bash
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

**Example 2**
```bash
Input: head = [2,1], x = 2
Output: [1,2]
```

### Constraints
- The number of nodes in the list is in the range [0, 200].
- -100 <= Node.val <= 100
- -200 <= x <= 200

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
 * @param {number} x
 * @return {ListNode}
 */
var partition = function(head, x) {
    if(!head) return head;

    let lesserList = new ListNode();
    let greaterList = new ListNode();
    let p = lesserList;
    let q = greaterList;
    let curr = head;

    while(curr) {
        if(curr.val < x) {
            p.next = curr;
            p = curr;
        } else {
            q.next = curr;
            q = curr;
        }
        curr = curr.next;
    }

    p.next = greaterList.next;
    q.next = null;

    return lesserList.next;
};
```
