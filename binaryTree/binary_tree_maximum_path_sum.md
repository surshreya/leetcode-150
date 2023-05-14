
##   Binary Tree Maximum Path Sum

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

**```The path sum of a path is the sum of the node's values in the path.```**

Given the ```root``` of a binary tree, return the ```maximum path sum of any non-empty path.```

![exx1](https://github.com/surshreya/leetcode-150/assets/118065908/d29b197f-ade1-4275-850b-d381a323e51f)

**Example 1**
```bash
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```
![exx2](https://github.com/surshreya/leetcode-150/assets/118065908/27a07a25-2cb0-41dc-9d0d-73894b3c7beb)

**Example 2**
```bash
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

### Constraints
- The number of nodes in the tree is in the range [1, 3 * 104].
- -1000 <= Node.val <= 1000

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
var maxPathSum = function(root) {
     let maxSum = -Infinity;

  const findMaxPathSum = (node) => {
        if (!node) {
        return 0;
        }

        const leftSum = findMaxPathSum(node.left);
        const rightSum = findMaxPathSum(node.right);

        const currSum = node.val + Math.max(leftSum, 0) + Math.max(rightSum, 0);
        maxSum = Math.max(maxSum, currSum);

        return node.val + Math.max(leftSum, rightSum, 0);
    };

    findMaxPathSum(root);
    return maxSum;
};
```
