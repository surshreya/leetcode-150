
##  Minimum Absolute Difference in BST

Given the ```root``` of a Binary Search Tree (BST), ```return the minimum absolute difference between the values of any two different nodes in the tree.```

![bst1](https://github.com/surshreya/leetcode-150/assets/118065908/be20c676-eb9a-4563-a5cd-054100935a91)

**Example 1**
```bash
Input: root = [4,2,6,1,3]
Output: 1
```

![bst2](https://github.com/surshreya/leetcode-150/assets/118065908/8c176630-e824-4650-9dfd-5d2e47c3666f)

**Example 2**
```bash
Input: root = [4,2,6,1,3]
Output: 1
```


### Constraints
- The number of nodes in the tree is in the range [2, 104].
- 0 <= Node.val <= 105

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

const inorder= (root, inorderArr) => {
    if(!root) return;
    inorder(root.left, inorderArr);
    inorderArr.push(root.val);
    inorder(root.right, inorderArr);
}
/**
 * @param {TreeNode} root
 * @return {number}
 */
var getMinimumDifference = function(root) {
    const inorderArr = [];
    inorder(root, inorderArr);
    let min = Infinity;

    for(let i=0; i<inorderArr.length - 1; i++) {
        min = Math.min(min, inorderArr[i+1] - inorderArr[i]);
    }
    return min;
};
```
