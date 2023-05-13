## Add Two Numbers

You are given two **_non-empty_** linked lists representing two non-negative integers. The digits are stored in **_reverse order_**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.
![addtwonumber1](https://user-images.githubusercontent.com/118065908/234662267-832eb2ae-f057-44f1-a909-1848e43346fe.jpg)

**Example 1**

```bash
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2**

```bash
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3**

```bash
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
```

### Constraints

- `The number of nodes in each linked list is in the range [1, 100].`
- `0 <= Node.val <= 9`
- `It is guaranteed that the list represents a number that does not have leading zeros.`

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
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function (l1, l2) {
  const lR = new ListNode();
  let temp = lR;
  let carry = 0;

  while (l1 || l2 || carry) {
    let sum = 0;

    if (l1) {
      sum += l1.val;
      l1 = l1.next;
    }

    if (l2) {
      sum += l2.val;
      l2 = l2.next;
    }

    sum += carry;
    carry = Math.floor(sum / 10);
    const node = new ListNode(Math.floor(sum % 10));
    temp.next = node;
    temp = temp.next;
  }

  return lR.next;
};
```
