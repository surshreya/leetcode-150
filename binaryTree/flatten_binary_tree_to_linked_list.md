
##  Flatten Binary Tree to Linked List

Given the ```root``` of a binary tree, flatten the tree into a "linked list":

- The "linked list" should use the same TreeNode class where the right child pointer points to the next node in the list and the left child pointer is always null.
- The "linked list" should be in the same order as a pre-order traversal of the binary tree.

![flaten](https://github.com/surshreya/leetcode-150/assets/118065908/67f972a0-ee75-43ce-97ed-352fc53de8f5)

**Example 1**
```bash
Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
```

**Example 2**
```bash
Input: root = []
Output: []
```

**Example 3**
```bash
Input: root = [0]
Output: [0]
```

### Constraints
- The number of nodes in the tree is in the range [0, 2000].
- -100 <= Node.val <= 100

**Follow up:** Can you flatten the tree in-place (with O(1) extra space)?



## Solution

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {void} Do not return anything, modify root in-place instead.
 */
var flatten = function(root) {
    if(!root) return;

    const stack = [root];
    let list = null;
    while(stack.length > 0) {
        const node = stack.pop();

        if (node.right) stack.push(node.right);
        if (node.left) stack.push(node.left);

        if(list) {
            list.left = null;
            list.right = node;
        }

        list = node;
    }
};
```
