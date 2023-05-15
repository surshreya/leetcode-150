
##    Kth Smallest Element in a BST

Given the ```root``` of a binary search tree, and an integer ```k```, return the kth smallest value ***```(1-indexed)```*** of all the values of the nodes in the tree.

 


 



![kthtree1](https://user-images.githubusercontent.com/118065908/234336257-9c312a0d-dfb4-40dd-bae4-edca70dec3d4.jpg)

**Example 1**
```bash
Input: root = [3,1,4,null,2], k = 1
Output: 1
```
![kthtree2](https://user-images.githubusercontent.com/118065908/234336266-caf7c279-6eab-4c11-9a48-78b86ade2f02.jpg)

**Example 2**
```bash
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```

### Constraints

- ```The number of nodes in the tree is n.```
- ```1 <= k <= n <= 104```
- ```0 <= Node.val <= 104```

### Follow Up

- ```You may only use constant extra space.```
- ```The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.```

## Solution

***Recursive***
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
 * @param {number} k
 * @return {number}
 */

 const inorderTraversal = (root, inorder) => {
     if(!root) return;

     inorderTraversal(root.left, inorder);
     inorder.push(root.val);
     inorderTraversal(root.right, inorder);
 }

var kthSmallest = function(root, k) {
    const inorder = [];
    inorderTraversal(root, inorder);
    return inorder[k-1];
};
```

***Iterative***
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
 * @param {number} k
 * @return {number}
 */
var kthSmallest = function(root, k) {
   if(!root) return;

   const stack = [root];
   let p = root;
   while(p || stack.length > 0) {
       if(p) {
           stack.push(p);
           p=p.left;
       } else {
           let node = stack.pop();
           k--;
           if(k === 0) return node.val;
           p=node.right;
       }
   }

   return;
};
```
