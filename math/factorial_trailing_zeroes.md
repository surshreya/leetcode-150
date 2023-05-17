## Factorial Trailing Zeroes

Given an integer `n`, return the number of **_`trailing zeroes in n!.`_**

**Note** that `n! = n * (n - 1) * (n - 2) * ... * 3 * 2 * 1.`

**Example 1**

```bash
Input: n = 3
Output: 0
Explanation: 3! = 6, no trailing zero.
```

**Example 2**

```bash
Input: n = 5
Output: 1
Explanation: 5! = 120, one trailing zero.
```

**Example 3**

```bash
Input: n = 0
Output: 0
```

### Constraints

- 0 <= n <= 104

## Solution

```javascript
/**
 * @param {number} n
 * @return {number}
 */
var trailingZeroes = function (n) {
  let trailingZeroCount = 0;

  for (let i = 5; Math.floor(n / i) >= 1; i *= 5) {
    trailingZeroCount += Math.floor(n / i);
  }

  return trailingZeroCount;
};
```
