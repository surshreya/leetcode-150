
##   Count Complete Tree Nodes

Given the ```root``` of a complete binary tree, return the number of the nodes in the tree.

According to Wikipedia, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between ```1 and 2h nodes``` inclusive at the last level ```h```.

```Design an algorithm that runs in less than O(n) time complexity.```


 ![complete](https://github.com/surshreya/leetcode-150/assets/118065908/a208e3b7-9a7b-4d7d-9503-1f5db49ef883)

**Example 1**
```bash
Input: root = [1,2,3,4,5,6]
Output: 6
```

**Example 2**
```bash
Input: root = []
Output: 0
```

**Example 2**
```bash
Input: root = [1]
Output: 1
```

### Constraints
- The number of nodes in the tree is in the range [1, 105].
- 0 <= Node.val <= 106
- The tree is guaranteed to be complete.


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
 * @return {number}
 */
var countNodes = function(root) {
  if (!root) return 0;

  let count = 0;
  const queue = [root];
  while (queue.length > 0) {
    const current = queue.shift();
    count += 1;
    if (current.left) queue.push(current.left);
    if (current.right) queue.push(current.right);
  }

  return count;
};
```
