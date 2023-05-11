
##   Valid Sudoku

Given an ```m x n``` matrix, return all elements of the matrix in ```spiral order```.


![spiral1](https://github.com/surshreya/leetcode/assets/118065908/d854c1e7-0dfe-4f64-8ec5-cced94d29e58)

**Example 1**
```bash
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

**Example 2**
```bash
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```
![spiral](https://github.com/surshreya/leetcode/assets/118065908/36632a2d-9185-4124-80e2-4c6669234a61)

### Constraints

- ```m == matrix.length```
- ```n == matrix[i].length```
- ```1 <= m, n <= 10```
- ```-100 <= matrix[i][j] <= 100```

## Solution

***``` Solution 1 ```***
```javascript

var spiralOrder = function(matrix) {
    const n = matrix.length;
    const m = matrix[0].length;
    let left = 0, right = m - 1;
    let top = 0, bottom = n - 1;
    const result = [];

    while(top<=bottom && left<=right) {
        for(let i = left; i <= right; i++) {
            result.push(matrix[top][i]);
        }
        top++;
        for(let i = top; i <= bottom; i++) {
            result.push(matrix[i][right]);
        }
        right--;
        if(top <= bottom) {
            for(let i = right; i >= left; i--) {
                result.push(matrix[bottom][i]);
            }
            bottom--;
        }

        if(left <= right) {
            for(let i = bottom;  i>=top; i--) {
                result.push(matrix[i][left]);
            }
            left++;
        }
    }

    return result;
};
```
