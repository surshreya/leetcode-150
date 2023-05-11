
##  Set Matrix Zeroes

Given an ```m x n``` integer matrix matrix, if an element is ```0```, set its ```entire row and column to 0's.```

You must do it in place.

 
![mat1 (1)](https://github.com/surshreya/leetcode/assets/118065908/3792b597-906c-47e2-9205-16b04ace0ab5)

**Example 1**
```bash
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```
![mat2 (1)](https://github.com/surshreya/leetcode/assets/118065908/7e9867f8-cd57-41a5-bd30-4aa0a8ed2202)

**Example 2**
```bash
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

### Constraints

- ```m == matrix.length```
- ```n == matrix[0].length```
- ```1 <= m, n <= 200```
- ```-231 <= matrix[i][j] <= 231 - 1```

### Follow up:

- A straightforward solution using O(mn) space is probably a bad idea.
- A simple improvement uses O(m + n) space, but still not the best solution.
- Could you devise a constant space solution?

## Solution

```javascript
var setZeroes = function(matrix) {
    const n = matrix.length;
    const m = matrix[0].length;

    const row = [];
    const column = [];

    for(let i=0;i<n;i++) {
        for(let j=0;j<m;j++) {
            if(matrix[i][j] === 0) {
                row[i]=1;
                column[j]=1;
            }
        }
    }

    for(let i=0;i<n;i++) {
        for(let j=0;j<m;j++) {
            if(row[i] ===1 || column[j] === 1) {
                matrix[i][j] = 0;
            }
        }
    }
};
```
