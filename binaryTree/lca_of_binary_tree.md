
##    Lowest Common Ancestor of a Binary Tree

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes ```p``` and ```q``` as the ***```lowest node in T```*** that has both p and q as descendants **(where we allow a node to be a descendant of itself)**.”
 


 


![binarytree](https://user-images.githubusercontent.com/118065908/234305099-500f0a2a-e514-48c9-a264-760e7e85ef1b.png)


**Example 1**
```bash
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```

![binarytree (1)](https://user-images.githubusercontent.com/118065908/234305122-cf6294bc-cac9-46cb-babd-2315a87f6866.png)

**Example 2**
```bash
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```
**Example 3**
```bash
Input: root = [1,2], p = 1, q = 2
Output: 1
```

### Constraints

- ```The number of nodes in the tree is in the range [2, 105].```
- ```-109 <= Node.val <= 109```
- ```All Node.val are unique.```
- ```p != q```
- ```p and q will exist in the tree```.

## Solution

```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function(root, p, q) {
    if(root===null||root===p||root===q) return root;
    
    let left = lowestCommonAncestor(root.left,p,q);
    let right = lowestCommonAncestor(root.right,p,q);

    if(left===null) return right;
    else if(right===null) return left;
    else return root;
};
```
