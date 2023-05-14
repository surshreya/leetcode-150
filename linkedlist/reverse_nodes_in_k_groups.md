
##    Reverse Nodes in k-Group

Given the ```head``` of a linked list, reverse the nodes of the list ```k``` at a time, and ```return the modified list.```

```k``` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

![reverse_ex1](https://github.com/surshreya/leetcode-150/assets/118065908/33dc28d7-ca79-48d8-a35a-01fb0bdbaf43)

**Example 1**
```bash
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

![reverse_ex2](https://github.com/surshreya/leetcode-150/assets/118065908/f1d2f64f-8ef9-42ae-a7b9-51da6c353545)

**Example 2**
```bash
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

### Constraints
- The number of nodes in the list is n.
- 1 <= k <= n <= 5000
- 0 <= Node.val <= 1000

**Follow-up:** Can you solve the problem in O(1) extra memory space?



## Solution

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
 const length = (head) => {
     let length = 0;
     while(head) {
         length += 1;
         head = head.next;
     }
     return length;
 }
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var reverseKGroup = function(head, k) {
    if(!head || !head.next) return head;

    let len = length(head);
    let dummy = new ListNode(0);
    dummy.next = head;
    let pre = dummy, cur = null, nex = null;
    while(len >= k) {
        cur = pre.next;
        nex = cur.next;

        for(let i=1;i<k;i++) {
            cur.next = nex.next;
            nex.next = pre.next;
            pre.next = nex;
            nex = cur.next;
        }
        pre = cur;
        len = len - k;
    }

    return dummy.next;
};
```
