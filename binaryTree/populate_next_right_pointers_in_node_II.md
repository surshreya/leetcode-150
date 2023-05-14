
##  Populating Next Right Pointers in Each Node II

Given a binary tree
```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to ```NULL```.

Initially, all next pointers are set to ```NULL```.
![117_sample](https://github.com/surshreya/leetcode-150/assets/118065908/d019684f-5599-436b-97fa-e94a16731bdf)

**Example 1**
```bash
Input: root = [1,2,3,4,5,null,7]
Output: [1,#,2,3,#,4,5,7,#]
Explanation: Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Example 2**
```bash
Input: root = []
Output: []
```

### Constraints
- You may only use constant extra space.
- The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.


## Solution

```javascript
/**
 * // Definition for a Node.
 * function Node(val, left, right, next) {
 *    this.val = val === undefined ? null : val;
 *    this.left = left === undefined ? null : left;
 *    this.right = right === undefined ? null : right;
 *    this.next = next === undefined ? null : next;
 * };
 */

/**
 * @param {Node} root
 * @return {Node}
 */
var connect = function(root) {
    if(!root) return null;
    if(root.length === 0) return [];
    
    let queue = [root];
    while(queue.length > 0) {
        const order = [];
        for(let i=0;i<queue.length;i++) {
            const current = queue[i];
            current.next = queue[i+1] || null;
            if (current.left) order.push(current.left);
            if (current.right) order.push(current.right);
        }
        queue = order;
    }

    return root;
};
```
