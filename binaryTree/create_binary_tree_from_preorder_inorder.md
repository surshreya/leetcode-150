
##     Construct Binary Tree from Preorder and Inorder Traversal

Given two integer arrays ```preorder``` and ```inorder``` where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, ```construct and return the binary tree.```
 


 
![tree](https://user-images.githubusercontent.com/118065908/233850653-be991083-5005-4f64-843d-53fa9916f530.jpg)




**Example 1**
```bash
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```
**Example 2**
```bash
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```

### Constraints

- 1 <= preorder.length <= 3000
- inorder.length == preorder.length
- -3000 <= preorder[i], inorder[i] <= 3000
- preorder and inorder consist of unique values.
- Each value of inorder also appears in preorder.
- preorder is guaranteed to be the preorder traversal of the tree.
- inorder is guaranteed to be the inorder traversal of the tree.


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
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */

 const buildBST = function(preorder, inorder)  {
     if(preorder.length === 0 || inorder.length === 0) {
         return null;
     }

     const rootVal = preorder[0];
     const rootIdx = inorder.indexOf(rootVal);
     
     const leftInorder = inorder.slice(0, rootIdx);
     const rightInorder = inorder.slice(rootIdx+1);

     const leftPreorder = preorder.slice(1, rootIdx+1);
     const rightPreorder = preorder.slice(rootIdx+1);

     const left = buildBST(leftPreorder, leftInorder);
     const right = buildBST(rightPreorder, rightInorder);
     const node = new TreeNode(rootVal, left, right);
     return node;
 }
var buildTree = function(preorder, inorder) {
    return buildBST(preorder, inorder);
};
```
