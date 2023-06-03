
## Minimum Path Sum

Given a ```m x n grid``` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

![minpath (1)](https://github.com/surshreya/leetcode-150/assets/118065908/baf76fb4-22fa-40a3-b1e7-b1408867e94f)

**Example 1**
```bash
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

**Example 2**
```bash
Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```

### Constraints

- m == grid.length
- n == grid[i].length
- 1 <= m, n <= 200
- 0 <= grid[i][j] <= 200

 
## Solution

```javascript
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function(grid) {
    const n = grid.length;
    const m = grid[0].length;
    const dp = new Array(n).fill(0).map(() => new Array(m).fill(0));
    
    for(let i=0;i<n;i++) {
        for(let j=0;j<m;j++) {
            if(i===0 && j===0) {
                dp[i][j] = grid[i][j];
            } else {
                let up= grid[i][j];
                if(i>0) {
                    up+=dp[i-1][j];
                } else {
                    up+=Infinity;
                }

                let left= grid[i][j];
                if(j>0) {
                    left+=dp[i][j-1];
                } else {
                    left+=Infinity;
                }

                dp[i][j] = Math.min(up, left);
            }
        }
    }
    return dp[n-1][m-1];
};
```
