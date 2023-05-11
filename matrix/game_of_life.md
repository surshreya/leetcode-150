
##  Game of Life

The board is made up of an ```m x n``` grid of cells, where each cell has an initial state: ```live (represented by a 1)``` or ```dead (represented by a 0)```. Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

- Any live cell with fewer than two live neighbors dies as if caused by under-population.
- Any live cell with two or three live neighbors lives on to the next generation.
- Any live cell with more than three live neighbors dies, as if by over-population.
- Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.


The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously. Given the current state of the m x n grid board, return the next state.
![grid1](https://github.com/surshreya/leetcode/assets/118065908/c4e37247-e04a-4153-9716-55881d6eb25e)

**Example 1**
```bash
Input: board = [[0,1,0],[0,0,1],[1,1,1],[0,0,0]]
Output: [[0,0,0],[1,0,1],[0,1,1],[0,1,0]]
```
![grid2](https://github.com/surshreya/leetcode/assets/118065908/5e7f8518-abd5-46fa-a151-afdaafad33ef)

**Example 2**
```bash
Input: board = [[1,1],[1,0]]
Output: [[1,1],[1,1]]
```

### Constraints

- ```m == board.length```
- ```n == board[i].length```
- ```1 <= m, n <= 25```
- ```board[i][j] is 0 or 1.```

### Follow up:

- Could you solve it in-place? Remember that the board needs to be updated simultaneously: You cannot update some cells first and then use their updated values to update other cells.
- In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches upon the border of the array (i.e., live cells reach the border). How would you address these problems?

## Solution

```javascript
const getNeighbor = (board, r, c, m, n) => {
    let count = 0;
    if(r > 0) {
        if(board[r-1][c] === 1 || board[r-1][c] === 2) count++;
        if(c > 0) {
            if(board[r-1][c-1] === 1 || board[r-1][c-1] === 2) count++;
        }
        if(c < n-1) {
            if(board[r-1][c+1] === 1 || board[r-1][c+1] === 2) count++;
        }
    }
    if(r+1 < m) {
        if(board[r+1][c] === 1 || board[r+1][c] === 2) count++;
        if(c > 0) {
            if(board[r+1][c-1] === 1 || board[r+1][c-1] === 2) count++;
        }
        if(c < n-1) {
            if(board[r+1][c+1] === 1 || board[r+1][c+1] === 2) count++;
        }
    }
    if(c > 0) {
        if(board[r][c-1] === 1 || board[r][c-1] === 2) count++;
    }
    if(c + 1 < n) {
        if(board[r][c+1] === 1 || board[r][c+1] === 2) count++;
    }

    return count;
}


/**
 * @param {number[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var gameOfLife = function(board) {
    if(!board || board.length === 0) return;

    let m = board.length;
    let n = board[0].length;
    
    for(let i = 0; i < m; i++) {
        for(let j=0; j<n;j++) {
            const neighbor = getNeighbor(board,i,j,m,n);
            if(board[i][j] === 1 && neighbor < 2) board[i][j] = 2;
            if(board[i][j] === 1 && neighbor > 3) board[i][j] = 2;
            if(board[i][j] === 0 && neighbor === 3) board[i][j] = 3;
        }
    }

    for(let i = 0; i < m; i++) {
        for(let j=0; j<n;j++) {
            if(board[i][j] === 2) board[i][j] = 0;
            if(board[i][j] === 3) board[i][j] = 1;
        }
    }
};
```
