
##  Sum Root to Leaf Numbers
 
You are given the ```root``` of a binary tree containing digits from ```0 to 9``` only.

Each ***root-to-leaf*** path in the tree represents a number.

```For example, the root-to-leaf path 1 -> 2 -> 3 represents the number 123.```

Return the total sum of all root-to-leaf numbers. Test cases are generated so that the answer will fit in a **32-bit integer**.

A **leaf** node is a node with no children.

 
![num1tree](https://github.com/surshreya/leetcode-150/assets/118065908/88dd2533-fff8-4731-81a7-8fc512f2be83)

**Example 1**
```bash
Input: root = [1,2,3]
Output: 25
Explanation:
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```
![num2tree](https://github.com/surshreya/leetcode-150/assets/118065908/dd13d2ee-831b-4b8d-9449-3f7aa179c5eb)

**Example 2**
```bash
Input: root = [4,9,0,5,1]
Output: 1026
Explanation:
The root-to-leaf path 4->9->5 represents the number 495.
The root-to-leaf path 4->9->1 represents the number 491.
The root-to-leaf path 4->0 represents the number 40.
Therefore, sum = 495 + 491 + 40 = 1026.
```

### Constraints
- The number of nodes in the tree is in the range [1, 1000].
- 0 <= Node.val <= 9
- The depth of the tree will not exceed 10

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
 * @return {number}
 */
var sumNumbers = function(root) {
     const sums = [];
    function dfs(root, sum) {
        if (!root) return;
        sum += root.val;
        if (!root.left && !root.right) {
        sums.push(sum);
        }

        dfs(root.left, sum);
        dfs(root.right, sum);
    }

    dfs(root, "");
    return sums.reduce((acc, cur) => acc + Number(cur), 0);
};
```
