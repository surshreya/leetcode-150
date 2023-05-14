## Binary Tree Level Order Traversal

Given the `root` of an binary tree, return the `level order traversal` of its nodes' values.

![tree1](https://user-images.githubusercontent.com/118065908/233822465-6968b8b2-2198-4571-978f-1fb05f0dc97b.jpg)
**Example 1**

```bash
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

**Example 2**

```bash
Input: root = [1]
Output: [[1]]
```

**Example 3**

```bash
Input: root = []
Output: []
```

### Constraints

- `The number of nodes in the tree is in the range [0, 2000].`
- `-1000 <= Node.val <= 1000`

## Solution

```cpp

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(root==NULL) {
            return res;
        }
        queue<TreeNode *> q;
        q.push(root);

        while(!q.empty()) {
            int size = q.size();
            vector<int> level;
            for(int i = 0; i < size; i++) {
                TreeNode *node = q.front();
                q.pop();
                if(node->left != NULL) q.push(node->left);
                if(node->right != NULL) q.push(node->right);
                level.push_back(node->val);
            }
            res.push_back(level);
        }
        return res;
    }
};

```

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
 * @return {number[][]}
 */
var levelOrder = function (root) {
  if (!root || root.length === 0) return [];

  const traversed = [];
  const queue = [root];

  while (queue.length > 0) {
    const size = queue.length;
    const level = [];
    for (let i = 0; i < size; i++) {
      const current = queue.shift();
      if (current.left) queue.push(current.left);
      if (current.right) queue.push(current.right);
      level.push(current.val);
    }
    traversed.push(level);
  }

  return traversed;
};
```
