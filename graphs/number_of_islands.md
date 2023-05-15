## Number of Islands

Given an `m x n` 2D binary grid `grid` which represents a map of **_`'1's (land) and '0's (water)`_**, return the `number of islands`.

An **_island_** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1**

```bash
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

**Example 2**

```bash
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

### Constraints

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j] is '0' or '1'.`

## Solution

**_Recursive_**

```javascript
/**
 * @param {character[][]} grid
 * @return {number}
 */
const explore = (grid, r, c, visited) => {
  const validRow = r >= 0 && r < grid.length;
  const validCol = c >= 0 && c < grid[0].length;

  if (!validRow || !validCol) return false;
  if (grid[r][c] === "0") return false;

  const pos = r + "," + c;
  if (visited.has(pos)) return false;

  visited.add(pos);
  explore(grid, r - 1, c, visited);
  explore(grid, r + 1, c, visited);
  explore(grid, r, c - 1, visited);
  explore(grid, r, c + 1, visited);

  return true;
};

var numIslands = function (grid) {
  const visited = new Set();
  let count = 0;
  for (let r = 0; r < grid.length; r++) {
    for (let c = 0; c < grid[0].length; c++) {
      if (explore(grid, r, c, visited) === true) {
        count += 1;
      }
    }
  }

  return count;
};
```
