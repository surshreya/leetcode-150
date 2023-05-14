
## Same Tree

Given the roots of two binary trees ```p``` and ```q```, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.
![ex1](https://github.com/surshreya/leetcode-150/assets/118065908/8b23e5bd-fc72-4df6-9f96-d7a9906263f0)

**Example 1**
```bash
Input: p = [1,2,3], q = [1,2,3]
Output: true
```
![ex2](https://github.com/surshreya/leetcode-150/assets/118065908/f871c769-8c9f-4ffd-ba63-a4c61e88025e)

**Example 2**
```bash
Input: p = [1,2], q = [1,null,2]
Output: false
```
![ex3](https://github.com/surshreya/leetcode-150/assets/118065908/e24cd4a6-a38d-4649-b0d2-ba8e2d434657)

**Example 3**
```bash
Input: p = [1,2,1], q = [1,1,2]
Output: false
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
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    if(!p || !q) return p == q;
    return p.val === q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
};
```
