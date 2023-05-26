## Bitwise AND of Numbers Range

Given two integers `left` and `right` that represent the range `[left, right]`, **_`return the bitwise AND of all numbers in this range, inclusive.`_**

**Example 1**

```bash
Input: left = 5, right = 7
Output: 4
```

**Example 2**

```bash
Input: left = 0, right = 0
Output: 0
```

**Example 3**

```bash
Input: left = 1, right = 2147483647
Output: 0
```

### Constraints

- 0 <= left <= right <= 231 - 1

## Solution

```javascript
/**
 * @param {number} left
 * @param {number} right
 * @return {number}
 */
var rangeBitwiseAnd = function (left, right) {
  let shift = 0;
  while (left != right && left > 0) {
    left >>= 1;
    right >>= 1;
    shift++;
  }

  left = left << shift;
  return left;
};
```
