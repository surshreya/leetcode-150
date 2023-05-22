
##  Search a 2D Matrix

You are given an m x n integer matrix ```matrix``` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

```Given an integer target, return true if target is in matrix or false otherwise.```

You must write a solution in ```O(log(m * n))``` time complexity.

![mat](https://github.com/surshreya/leetcode-150/assets/118065908/9d9aefc0-64d7-4aa3-8829-b8f3b74f405c)

**Example 1**
```bash
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

![mat2 (2)](https://github.com/surshreya/leetcode-150/assets/118065908/fbde3e95-fdd0-4ee4-bc19-86c1599a6977)

**Example 2**
```bash
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```


### Constraints
- m == matrix.length
- n == matrix[i].length
- 1 <= m, n <= 100
- -104 <= matrix[i][j], target <= 104

## Solution

```javascript
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function(matrix, target) {
    const m = matrix.length;
    const n = matrix[0].length;

    let l = 0, h = (m*n)-1;
    while(l<=h) {
        let mid = l +Math.floor(h-l/2);
        if(matrix[Math.floor(mid / n)][mid%n] === target) {
            return true;
        } else if(matrix[Math.floor(mid / n)][mid%n] < target) {
            l = mid + 1;
        } else {
            h = mid - 1;
        }
    }
    return false;
};
```
