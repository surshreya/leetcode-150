
##   N-Queens

The **n-queens puzzle** is the problem of placing ```n``` queens on an ```n x n``` chessboard such that ```no two queens attack each other```.

Given an integer ```n```, return ***```all distinct solutions to the n-queens puzzle```***. You may return the answer in **any order**.

Each solution contains a distinct board configuration of the n-queens' placement, where ```'Q'``` and ```'.'``` both indicate a queen and an empty space, respectively.

![queens](https://github.com/surshreya/leetcode-150/assets/118065908/262e7dcf-cd2f-47a6-bf9a-a0b960163cc6)

**Example 1**
```bash
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
Explanation: There exist two distinct solutions to the 4-queens puzzle as shown above
```

**Example 2**
```bash
Input: n = 1
Output: [["Q"]]
```

### Constraints

- ```1 <= n <= 9```

## Solution
```javascript
const solve = (col, board, result, leftRow, upperDiag, lowerDiag, n) => {
    if(col === n) {
        result.push(board.map(row => row.join('')));
        return;
    }

    for(let row=0;row<n;row++) {
        if(leftRow[row] === 0 && lowerDiag[row+col]===0&& upperDiag[n-1+col-row]===0) {
            board[row][col] = 'Q';
            leftRow[row] = 1;
            lowerDiag[row+col]=1;
            upperDiag[n-1+col-row]=1;
            solve(col+1,board,result,leftRow,upperDiag,lowerDiag,n);
            board[row][col] = '.';
            leftRow[row] = 0;
            lowerDiag[row+col]=0;
            upperDiag[n-1+col-row]=0;
        }
    }
}

/**
 * @param {number} n
 * @return {string[][]}
 */
var solveNQueens = function(n) {
    const result = [];
    const board = Array.from({ length: n }, () => Array(n).fill('.'));
    
    const leftRow = Array(n).fill(0);
    const upperDiag = Array(2*n-1).fill(0);
    const lowerDiag = Array(2*n-1).fill(0);
   
    solve(0,board,result,leftRow,upperDiag,lowerDiag,n);
    return result;
};
```

