
##    Populating Next Right Pointers in Each Node

You are given a **perfect binary tree** where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
```

Populate each next pointer to point to its ***```next right node```***. If there is no next right node, the next pointer should be set to ```NULL```.

Initially, all next pointers are set to ```NULL```.
 


 

![116_sample](https://user-images.githubusercontent.com/118065908/234322241-2dd99078-15ba-46f6-9d55-5f3553c5b26d.png)



**Example 1**
```bash
Input: root = [1,2,3,4,5,6,7]
Output: [1,#,2,3,#,4,5,6,7,#]
Explanation: Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
```

**Example 2**
```bash
Input: root = []
Output: []
```

### Constraints

- ```The number of nodes in the tree is in the range [0, 212 - 1].```
- ```-1000 <= Node.val <= 1000```

### Follow Up

- ```You may only use constant extra space.```
- ```The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.```

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
