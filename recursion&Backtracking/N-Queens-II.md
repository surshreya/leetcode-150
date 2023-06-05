
##   N-Queens-II

The **n-queens puzzle** is the problem of placing ```n``` queens on an ```n x n``` chessboard such that ***```no two queens attack each other.```***

```Given an integer n, return the number of distinct solutions to the n-queens puzzle.```

![queens](https://github.com/surshreya/leetcode-150/assets/118065908/be658341-231d-40f4-b6e8-1542da6f7c5b)

**Example 1**
```bash
Input: n = 4
Output: 2
Explanation: There are two distinct solutions to the 4-queens puzzle as shown.
```

**Example 2**
```bash
Input: n = 1
Output: 1
```

### Constraints

- ```1 <= n <= 9```

## Solution
```javascript
const solve = (col, board, result, leftRow, upperDiag, lowerDiag, n, count) => {
    if(col === n) {
        count++;
        return count;
    }

    for(let row=0;row<n;row++) {
        if(leftRow[row] === 0 && lowerDiag[row+col]===0&& upperDiag[n-1+col-row]===0) {
            board[row][col] = 'Q';
            leftRow[row] = 1;
            lowerDiag[row+col]=1;
            upperDiag[n-1+col-row]=1;
            count=solve(col+1,board,result,leftRow,upperDiag,lowerDiag,n, count);
            board[row][col] = '.';
            leftRow[row] = 0;
            lowerDiag[row+col]=0;
            upperDiag[n-1+col-row]=0;
        }
    }

    return count;
}
/**
 * @param {number} n
 * @return {number}
 */
var totalNQueens = function(n) {
    const result = [];
    const board = Array.from({ length: n }, () => Array(n).fill('.'));
    
    const leftRow = Array(n).fill(0);
    const upperDiag = Array(2*n-1).fill(0);
    const lowerDiag = Array(2*n-1).fill(0);
   
    const count = solve(0,board,result,leftRow,upperDiag,lowerDiag,n, 0);
    return count;
};
```

