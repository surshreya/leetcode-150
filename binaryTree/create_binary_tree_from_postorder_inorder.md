
##  Construct Binary Tree from Inorder and Postorder Traversal

Given two integer arrays ```inorder``` and ```postorder``` where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and ```return the binary tree```.

 
![tree (1)](https://github.com/surshreya/leetcode-150/assets/118065908/0d2f6b13-36f1-459a-92cc-8639bb0c090c)


**Example 1**
```bash
Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
Output: [3,9,20,null,null,15,7]
```

**Example 2**
```bash
Input: inorder = [-1], postorder = [-1]
Output: [-1]
```

### Constraints
- 1 <= inorder.length <= 3000
- postorder.length == inorder.length
- -3000 <= inorder[i], postorder[i] <= 3000
- inorder and postorder consist of unique values.
- Each value of postorder also appears in inorder.
- inorder is guaranteed to be the inorder traversal of the tree.
- postorder is guaranteed to be the postorder traversal of the tree

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

 const buildBST = function(postorder, inorder)  {
     if(postorder.length === 0 || inorder.length === 0) {
         return null;
     }

     const rootVal = postorder[postorder.length - 1];
     const rootIdx = inorder.indexOf(rootVal);
     
     const leftInorder = inorder.slice(0, rootIdx);
     const rightInorder = inorder.slice(rootIdx+1);

     const leftPostorder = postorder.slice(0, rootIdx);
     const rightPostorder = postorder.slice(rootIdx, postorder.length - 1);

     const left = buildBST(leftPostorder, leftInorder);
     const right = buildBST(rightPostorder, rightInorder);
     const node = new TreeNode(rootVal, left, right);
     return node;
 }

/**
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function(inorder, postorder) {
    return buildBST(postorder, inorder);
};
```
