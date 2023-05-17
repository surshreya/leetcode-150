## Palindrome Number

Given an integer `x`, return `true` if x is a **palindrome**, and `false` otherwise.

**Example 1**

```bash
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
```

**Example 2**

```bash
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3**

```bash
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

### Constraints

- -231 <= x <= 231 - 1

## Solution

```javascript
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function (x) {
  if (x < 0) return false;

  const num = x.toString();
  let i = 0,
    n = num.length - 1;
  while (i < n) {
    if (num[i] !== num[n]) {
      return false;
    }
    i++;
    n--;
  }
  return true;
};
```
