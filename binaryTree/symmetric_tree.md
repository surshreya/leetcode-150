## Symmetric Tree

Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

**Example 1**

```bash
Input: root = [1,2,2,3,4,4,3]
Output: true
```

**Example 2**

```bash
Input: root = [1,2,2,null,3,null,3]
Output: false
```

### Constraints

- `The number of nodes in the tree is in the range [1, 1000].`
- `-100 <= Node.val <= 100`

## Solution

```javascript
const isMirror = (n1, n2) => {
  if (n1 === null && n2 === null) return true;
  else if (n1 === null || n2 === null) return false;
  else if (n1.val !== n2.val) return false;
  return isMirror(n1.left, n2.right) && isMirror(n1.right, n2.left);
};

var isSymmetric = function (root) {
  return root === null || isMirror(root.left, root.right);
};
```
