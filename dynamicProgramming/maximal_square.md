
##  Maximal Square

Given an ```m x n``` binary matrix filled with ```0```'s and ```1```'s, find the ```largest square containing only 1's and return its area.```

 ![max1grid](https://github.com/surshreya/leetcode-150/assets/118065908/ea74bd4b-20e2-4087-875a-a3b6215e62ce)


**Example 1**
```bash
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4
```

![max2grid](https://github.com/surshreya/leetcode-150/assets/118065908/47446240-b28e-4a20-b33b-acd1c18c4490)

**Example 2**
```bash
Input: matrix = [["0","1"],["1","0"]]
Output: 1
```

**Example 3**
```bash
Input: matrix = [["0"]]
Output: 0
```

### Constraints

- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 300
- matrix[i][j] is '0' or '1'.
 
## Solution

```javascript
/**
 * @param {character[][]} matrix
 * @return {number}
 */
var maximalSquare = function(matrix) {
    const m = matrix.length;
    const n = matrix[0].length;
    let maxSquare = 0;

    const dp = new Array(m).fill(0).map(() => new Array(n).fill(0));

    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            if (matrix[i][j] === '0') {
                continue;
            }
            if (i === 0 || j === 0) {
                dp[i][j] = 1;
            } else {
                dp[i][j] = Math.min(dp[i][j - 1], dp[i - 1][j]);
                dp[i][j] = 1 + Math.min(dp[i][j], dp[i - 1][j - 1]);
            }
            if (dp[i][j] > maxSquare) {
                maxSquare = dp[i][j];
            }
        }
    }
    return maxSquare*maxSquare;
};
    
```

