
## Unique Paths II

You are given an ```m x n``` integer array grid. There is a robot initially located at the **top-left corner** (i.e., ```grid[0][0]```). The robot tries to move to the **bottom-right corner** (i.e., ```grid[m - 1][n - 1]```). The robot can only move either down or right at any point in time.

An obstacle and space are marked as ```1``` or ```0``` respectively in ```grid```. A path that the robot takes cannot include **any** square that is an obstacle.

```Return the number of possible unique paths that the robot can take to reach the bottom-right corner.```

The testcases are generated so that the answer will be less than or equal to 2 * 109.

 
![robot1](https://github.com/surshreya/leetcode-150/assets/118065908/677a1f9f-fde7-4040-ab46-b1b0b9056369)

**Example 1**
```bash
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

![robot2](https://github.com/surshreya/leetcode-150/assets/118065908/1acbe35b-915e-4487-9e90-e152ee00033c)

**Example 2**
```bash
Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```

### Constraints

- m == obstacleGrid.length
- n == obstacleGrid[i].length
- 1 <= m, n <= 100
- obstacleGrid[i][j] is 0 or 1.
 
## Solution

```javascript
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    const m = obstacleGrid.length;
    const n = obstacleGrid[0].length;

    const dp = [];
    for (let i = 0; i < m; i++) {
        dp.push(new Array(n).fill(0));
    }

    for (let i = 0; i < m; i++) {
        if (obstacleGrid[i][0] === 1) break;
        dp[i][0] = 1;
    }
    for (let j = 0; j < n; j++) {
        if (obstacleGrid[0][j] === 1) break;
        dp[0][j] = 1;
    }

    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (obstacleGrid[i][j] === 1) continue;
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }
    return dp[m-1][n-1];
};
```
