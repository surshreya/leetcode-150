
##  Rotate Image

You are given an ```n x n``` **2D** matrix representing an image, ***```rotate the image by 90 degrees (clockwise)```***.

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.
![mat1](https://github.com/surshreya/leetcode/assets/118065908/0a893714-1db1-4989-9e33-586dc2dff0e6)

**Example 1**
```bash
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]
```
![mat2](https://github.com/surshreya/leetcode/assets/118065908/a2cfae88-0505-49ed-8f16-728bcfededb2)

**Example 2**
```bash
Input: matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
Output: [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
```

### Constraints

- ```n == matrix.length == matrix[i].length```
- ```1 <= n <= 20```
- ```-1000 <= matrix[i][j] <= 1000```

## Solution

```javascript
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    const n = matrix.length;
    const m = matrix[0].length;

    for(let i=0;i<n;i++) {
        for(let j=0;j<i;j++) {
           [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]];
        }
    }

    for(let i=0;i<n;i++) {
        matrix[i].reverse();
    }

   return matrix;
};
```
