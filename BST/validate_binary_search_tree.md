
##    Validate Binary Search Tree

Given the ```root``` of a binary tree, determine if it is a ***```valid binary search tree (BST)```***.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.
 
 


 
![tree1 (2)](https://user-images.githubusercontent.com/118065908/233846828-82dc2097-1bff-4906-89dd-9216317f6dd2.jpg)




**Example 1**
```bash
Input: root = [2,1,3]
Output: true
```
![tree2](https://user-images.githubusercontent.com/118065908/233846839-d5f8e185-61ae-4536-b282-6b34cad39449.jpg)

**Example 2**
```bash
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

### Constraints

- ```The number of nodes in the tree is in the range [1, 104].```
- ```-231 <= Node.val <= 231 - 1```


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
 * @return {boolean}
 */
const validBST = (root, min, max) => {
    if(root === null) return true;
    
    if((min !== null && root.val <= min ) || (max !== null && root.val >= max)) {
        return false;
    }

    return validBST(root.left, min, root.val) && validBST(root.right, root.val, max);

 }
var isValidBST = function(root) {
    return validBST(root, null, null);
};
```
