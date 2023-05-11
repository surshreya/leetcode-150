## Valid Sudoku

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated **according to the following rules:**

- Each row must contain the digits 1-9 without repetition.
- Each column must contain the digits 1-9 without repetition.
- Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

**_Note:_**

- A Sudoku board (partially filled) could be valid but is not necessarily solvable.
- Only the filled cells need to be validated according to the mentioned rules.

**Example 1**

![image](https://github.com/surshreya/leetcode/assets/118065908/cff7d616-5774-44b4-86c4-e0cb255fdef4)


```bash
Input: board =
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2**

```bash
Input: board =
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```

### Constraints

- `board.length == 9`
- `board[i].length == 9`
- `board[i][j] is a digit 1-9 or '.'.`

## Solution

**_`Solution 1`_**

```javascript
var isValidSudoku = function (board) {
  //Valid Row
  for (let i = 0; i < 9; i++) {
    let row = new Map();
    for (let j = 0; j < 9; j++) {
      if (board[i][j] !== ".") {
        if (row.has(board[i][j])) {
          return false;
        } else {
          row.set(board[i][j], true);
        }
      }
    }
  }

  //Valid Column
  for (let i = 0; i < 9; i++) {
    let column = new Map();
    for (let j = 0; j < 9; j++) {
      if (board[j][i] !== ".") {
        if (column.has(board[j][i])) {
          return false;
        } else {
          column.set(board[j][i], true);
        }
      }
    }
  }

  //Valid sub box
  for (let i = 0; i < 9; i += 3) {
    for (let j = 0; j < 9; j += 3) {
      const subBox = new Map();
      for (let k = 0; k < 3; k++) {
        for (let l = 0; l < 3; l++) {
          const row = i + k;
          const column = j + l;
          if (board[row][column] !== ".") {
            if (subBox.has(board[row][column])) {
              return false;
            } else {
              subBox.set(board[row][column], true);
            }
          }
        }
      }
    }
  }

  return true;
};
```
