
##  Rotate List

Given the ```head``` of a linked list, rotate the list to the right by ```k``` places.

![rotate1](https://github.com/surshreya/leetcode-150/assets/118065908/53c55819-9694-40c9-9261-784b63ef9788)

**Example 1**
```bash
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```
![roate2](https://github.com/surshreya/leetcode-150/assets/118065908/fad8e433-65f1-447e-9d7f-b2689dc441a2)

**Example 2**
```bash
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

### Constraints

- The number of nodes in the list is in the range [0, 500].
- -100 <= Node.val <= 100
- 0 <= k <= 2 * 109

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
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function(head, k) {
    if (head === null || k === 0) {
      return head;
    }
  
    let temp = head;
    let len = 1, end = 0;
  
    while (temp.next !== null) {
      len++;
      temp = temp.next;
    }
    
    temp.next = head;
    k = k % len;
    end = len - k;
  
    while (end !== 0) {
      temp = temp.next;
      end--;
    }
  
    head = temp.next;
    temp.next = null;
  
    return head;
};
```
