
##    Surrounded Regions

Given an ```m x n``` matrix board containing ```'X'``` and ```'O'```, capture all regions that are ***```4-directionally surrounded by 'X'```***.

```A region is captured by flipping all 'O's into 'X's in that surrounded region.```

 


 


![xogrid](https://user-images.githubusercontent.com/118065908/234641524-31d5fc87-1fab-4da6-a6a1-8bb2dca154de.jpg)


**Example 1**
```bash
Input: board = [["X","X","X","X"],["X","O","O","X"],["X","X","O","X"],["X","O","X","X"]]
Output: [["X","X","X","X"],["X","X","X","X"],["X","X","X","X"],["X","O","X","X"]]
Explanation: Notice that an 'O' should not be flipped if:
- It is on the border, or
- It is adjacent to an 'O' that should not be flipped.
The bottom 'O' is on the border, so it is not flipped.
The other three 'O' form a surrounded region, so they are flipped.
```

**Example 2**
```bash
Input: board = [["X"]]
Output: [["X"]]
```

### Constraints

- ```m == grid.length```
- ```n == grid[i].length```
- ```1 <= m, n <= 200```
- ```board[i][j] is 'X' or 'O'.```


## Solution

***Recursive***
```javascript
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
const dfs = (board, r, c, visited) => {
  const validRow = r >= 0 && r < board.length;
  const validCol = c >= 0 && c < board[0].length;

  if (!validRow || !validCol) return;

  const pos = r + "," + c;
  if (board[r][c] === "X" || visited.has(pos)) return;

  visited.add(pos);
  dfs(board, r - 1, c, visited);
  dfs(board, r + 1, c, visited);
  dfs(board, r, c - 1, visited);
  dfs(board, r, c + 1, visited);
};

var solve = function(board) {
    let r = board.length;
    let c = board[0].length;

    let pos = "";
    const visited = new Set();

    for(let i = 0; i < r; i++) {
        pos = i + "," + 0;
        if(!visited.has(pos) && board[i][0] === 'O') {
            dfs(board, i, 0, visited);
        }
        pos = i + "," + c-1;
        if(!visited.has(pos) && board[i][c-1] === 'O') {
            dfs(board, i, c-1, visited);
        }
    }

    for(let j = 0; j < c; j++) {
        pos = 0 + "," + j;
        if(!visited.has(pos) && board[0][j] === 'O') {
            dfs(board, 0, j, visited);
        }
        pos = r-1 + "," + j;
        if(!visited.has(pos) && board[r-1][j] === 'O') {
            dfs(board, r-1, j, visited);
        }
    }


    for(let i=0;i<r;i++) {
        for(let j=0;j<c;j++) {
            pos = i + "," + j;
            if(!visited.has(pos) && board[i][j] === 'O') {
                board[i][j] = 'X';
            }
        }
    }
};
```
