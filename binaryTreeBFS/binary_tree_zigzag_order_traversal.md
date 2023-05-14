
##   Binary Tree Zigzag Level Order Traversal

Given the ```root``` of a binary tree, return the ***```zigzag level order traversal```*** of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

 
 


 ![tree1 (1)](https://user-images.githubusercontent.com/118065908/233845736-61eddb64-f69d-4026-8955-bb0c675aaa3f.jpg)





**Example 1**
```bash
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
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

- ```The number of nodes in the tree is in the range [0, 2000].```
- ```-1000 <= Node.val <= 1000```


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
 * @return {number[][]}
 */
var zigzagLevelOrder = function(root) {
    if(!root || root.length === 0) return [];

    const queue = [root];
    const traversal = [];
    let levelIdx = 1;
    while(queue.length > 0) {
        const size = queue.length;
        const level = [];
        for(let i = 0; i < size; i++) {
            const current = queue.shift();
            if(levelIdx % 2 ===0) {
                level.unshift(current.val);
            } else {
                level.push(current.val);
            }

            if(current.left) queue.push(current.left);
            if(current.right) queue.push(current.right);
        }
        levelIdx++;
        traversal.push(level);
    }
    return traversal;
};
```
