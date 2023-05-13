
##  Remove Duplicates from Sorted List II

Given the ```head``` of a sorted linked list, ```delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list```. Return **```the linked list sorted as well```**.

 ![linkedlist1](https://github.com/surshreya/leetcode/assets/118065908/787fbf05-e956-46a0-bdf9-7bba2408c502)


**Example 1**
```bash
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```
![linkedlist2](https://github.com/surshreya/leetcode/assets/118065908/994d70da-d67c-4b7d-afe6-c8c1c6b21367)

**Example 2**
```bash
Input: head = [1,1,1,2,3]
Output: [2,3]
```

### Constraints
- The number of nodes in the list is in the range [0, 300].
- -100 <= Node.val <= 100
- The list is guaranteed to be sorted in ascending order.

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
 * @return {ListNode}
 */
var deleteDuplicates = function(head) {
    if(!head) return head;

    let prev = null, cur = head;
    while(cur) {
        if(cur.next && cur.val === cur.next.val) {
            while(cur.next && cur.val === cur.next.val) {
                cur = cur.next;
            }

            if(prev) {
                prev.next = cur.next
            } else {
                head = cur.next
            }
        } else {
            prev = cur;
        }

        cur = cur.next;
    }

    return head;
};
```
