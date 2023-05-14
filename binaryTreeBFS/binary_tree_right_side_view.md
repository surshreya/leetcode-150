
##    Binary Tree Right Side View

Given the ```root``` of a binary tree, imagine yourself standing on the **right side** of it, ```return the values of the nodes you can see ordered from top to bottom.```

![tree (2)](https://github.com/surshreya/leetcode-150/assets/118065908/2094bf6a-63f1-4086-90f0-15fbb5d867a6)

**Example 1**
```bash
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

**Example 2**
```bash
Input: root = [1,null,3]
Output: [1,3]
```

**Example 3**
```bash
Input: root = []
Output: []
```

### Constraints
- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100


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
 * @return {number[]}
 */
var rightSideView = function(root) {
    if(!root || root.length === 0) return [];

    const result = [];
    const queue = [root];

    while(queue.length > 0) {
        const size = queue.length;
        for(let i = 0 ; i < size; i++) {
            const current = queue.shift();

            if(i === size - 1) {
                result.push(current.val);
            }
            if(current.left) queue.push(current.left);
            if(current.right) queue.push(current.right);
        }
    }

    return result;
};
```
