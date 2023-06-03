## Longest Palindromic Substring

Given a string `s`, return `the longest 
palindromic substring in s.`

**Example 1**

```bash
Input: s = "babad"
Output: "bab"
Explanation: "aba" is also a valid answer.
```

**Example 2**

```bash
Input: s = "cbbd"
Output: "bb"
```

### Constraints

- 1 <= s.length <= 1000
- s consist of only digits and English letters..

## Solution

**_`Solution 1`_**

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  const n = s.length;
  let start = 0;
  let end = 1;
  let low, hi;

  for (let i = 0; i < n; i++) {
    low = i - 1;
    hi = i;

    while (low >= 0 && hi < n && s[low] === s[hi]) {
      if (hi - low + 1 > end) {
        start = low;
        end = hi - low + 1;
      }
      low--;
      hi++;
    }

    low = i - 1;
    hi = i + 1;

    while (low >= 0 && hi < n && s[low] === s[hi]) {
      if (hi - low + 1 > end) {
        start = low;
        end = hi - low + 1;
      }
      low--;
      hi++;
    }
  }

  return s.slice(start, start + end);
};
```

**_`Solution 2 - DP`_**

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  const n = s.length;
  const dp = [];

  for (let i = 0; i < n; i++) {
    dp.push(new Array(n).fill(false));
  }

  let start = 0;
  let maxLength = 1;

  for (let i = 0; i < n; i++) {
    dp[i][i] = true;
  }

  for (let i = 0; i < n - 1; i++) {
    if (s[i] === s[i + 1]) {
      dp[i][i + 1] = true;
      start = i;
      maxLength = 2;
    }
  }

  for (let len = 3; len <= n; len++) {
    for (let i = 0; i < n - len + 1; i++) {
      const j = i + len - 1;
      if (s[i] === s[j] && dp[i + 1][j - 1]) {
        dp[i][j] = true;
        start = i;
        maxLength = len;
      }
    }
  }
  return s.slice(start, start + maxLength);
};
```
