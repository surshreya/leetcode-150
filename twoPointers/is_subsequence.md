
##  Is Subsequence

Given two strings s and t, return true if s is a **subsequence** of t, or false otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. ```(i.e., "ace" is a subsequence of "abcde" while "aec" is not).```

 




**Example 1**
```bash
Input: s = "abc", t = "ahbgdc"
Output: true
```
**Example 2**
```bash
Input: s = "axc", t = "ahbgdc"
Output: false
```
    
### Constraints

- ```0 <= s.length <= 100```
- ```0 <= t.length <= 104```
- ```s and t consist only of lowercase English letters.```

## Solution

```javascript
var isSubsequence = function(s, t) {
    let m = t.length, n = s.length;
    if(n==0) return true;

    let pIdx = 0, sIdx = 0;
    while(pIdx < m) {
        if(t[pIdx] === s[sIdx]) {
            sIdx++;
        }

        if(sIdx === n) return true;
        pIdx++;
    }
    return false;
};
```
