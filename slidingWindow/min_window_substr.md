
##   Minimum Window Substring

Given two strings ```s``` and ```t``` of lengths ```m``` and ```n``` respectively, ***```return the minimum window substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".```***

The testcases will be generated such that the answer is **unique.**

**Example 1**
```bash
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

**Example 2**
```bash
Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
```

**Example 3**
```bash
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```

### Constraints

- ```m == s.length```
- ```n == t.length```
- ```1 <= m, n <= 105```
- ```s and t consist of uppercase and lowercase English letters.```

**Follow up:** Could you find an algorithm that runs in ```O(m + n)``` time?
 
## Solution
```javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
var minWindow = function(s, t) {
    const targetMap = {};
    const windowMap = {};
    let currentCount = 0, targetCount = t.length;
    let result = '';

    for(const char of t) {
        targetMap[char] = (targetMap[char] || 0) + 1;
    }

    let left = 0, right = 0;
    while(right < s.length) {
        const char = s[right];

        if (targetMap[char]) {
            windowMap[char] = (windowMap[char] || 0) + 1
            if (windowMap[char] <= targetMap[char]) {
                currentCount += 1;
            }
        }

         while (currentCount >= targetCount && (windowMap[s[left]] > targetMap[s[left]] || !targetMap[s[left]])
        ) 
        {
            if (windowMap[s[left]] > targetMap[s[left]]) {
                windowMap[s[left]] -= 1;
            }
            left += 1;
        }
        if (currentCount >= targetCount) {
            if (result === '') {
                result = s.slice(left, right + 1);
            } else {
                result = right - left + 1 < result.length ? s.slice(left, right + 1) : result;
            }
        }
        right++;
    }
    return result;
};
```

