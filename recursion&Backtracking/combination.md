## Combinations

Given two integers `n` and `k`, return **_`all possible combinations of k numbers chosen from the range [1, n].`_**

You may return the answer in **any order**.

**Example 1**

```bash
Input: n = 4, k = 2
Output: [[1,2],[1,3],[1,4],[2,3],[2,4],[3,4]]
Explanation: There are 4 choose 2 = 6 total combinations.
Note that combinations are unordered, i.e., [1,2] and [2,1] are considered to be the same combination.
```

**Example 2**

```bash
Input: n = 1, k = 1
Output: [[1]]
Explanation: There is 1 choose 1 = 1 total combination.
```

### Constraints

- 1 <= n <= 20
- 1 <= k <= n

## Solution

```javascript
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */

const findCombination = (cur, i, k, n, result) => {
  if (cur.length === k) {
    result.push([...cur]);
    return;
  }

  for (let j = i; j <= n; j++) {
    cur.push(j);
    findCombination(cur, j + 1, k, n, result);
    cur.pop();
  }
};
var combine = function (n, k) {
  const result = [];
  findCombination([], 1, k, n, result);
  return result;
};
```
