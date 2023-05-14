
## Invert Binary Tree

Given the root of a binary tree, ```invert``` the tree, and return its root.

![invert1-tree](https://github.com/surshreya/leetcode-150/assets/118065908/3e3aac3e-e36b-41f4-b1fa-f35587533b9f)


**Example 1**
```bash
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```

**Example 2**
```bash
Input: root = [2,1,3]
Output: [2,3,1]
```
![invert2-tree](https://github.com/surshreya/leetcode-150/assets/118065908/5be156d5-8828-4ad0-b4cf-8ac8f421fd79)

**Example 3**
```bash
Input: root = []
Output: []
```

### Constraints
- The number of nodes in both trees is in the range [0, 100].
- -104 <= Node.val <= 104

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
 * @return {TreeNode}
 */
var invertTree = function(root) {
    if(!root || (!root.left && !root.right)) return root;

    let temp = root.left;
    root.left = root.right;
    root.right = temp;

    invertTree(root.left);
    invertTree(root.right);
    return root;
};
```
