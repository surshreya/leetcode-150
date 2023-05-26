## Generate Parentheses

Given `n` pairs of parentheses, write a function to generate `all combinations` of well-formed parentheses.

**Example 1**

```bash
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

**Example 2**

```bash
Input: n = 1
Output: ["()"]
```

### Constraints

- `1 <= n <= 8`

## Solution

```javascript
/**
 * @param {number} n
 * @return {string[]}
 */

const generate = (result, str, left, right, n) => {
  if (left === n && right === n) {
    result.push(str);
    return;
  }
  if (left < n) {
    generate(result, str + "(", left + 1, right, n);
  }
  if (left > right) {
    generate(result, str + ")", left, right + 1, n);
  }
};

var generateParenthesis = function (n) {
  const result = [];
  generate(result, "", 0, 0, n);
  return result;
};
```
