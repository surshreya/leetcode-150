
##   Average of Levels in Binary Tree

Given the ```root``` of a binary tree, return **```the average value of the nodes on each level in the form of an array```**. Answers within 10-5 of the actual answer will be accepted.
 
![avg1-tree](https://github.com/surshreya/leetcode-150/assets/118065908/63dbf7d8-9f28-4703-8ae1-d1a5ec5ca713)

**Example 1**
```bash
Input: root = [3,9,20,null,null,15,7]
Output: [3.00000,14.50000,11.00000]
Explanation: The average value of nodes on level 0 is 3, on level 1 is 14.5, and on level 2 is 11.
Hence return [3, 14.5, 11].
```
![avg2-tree](https://github.com/surshreya/leetcode-150/assets/118065908/5c233338-7b91-40ad-b8e0-d471f70e74f3)

**Example 2**
```bash
Input: root = [3,9,20,15,7]
Output: [3.00000,14.50000,11.00000]
```


### Constraints
- The number of nodes in the tree is in the range [1, 104].
- -231 <= Node.val <= 231 - 1


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
var averageOfLevels = function(root) {
     if(!root || root.length === 0) return [];

    const avgLevel = [];
    const queue = [root];

    while(queue.length > 0) {
        const size = queue.length;
        let sum = 0;
        let count = 0;
        for(let i = 0 ; i < size; i++) {
            const current = queue.shift();
            if(current.left) queue.push(current.left);
            if(current.right) queue.push(current.right);
            sum+=current.val;
            count+=1;
        }
        avgLevel.push(sum/count);        
    }
    return avgLevel;
};
```
