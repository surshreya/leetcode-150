
##  Longest Substring Without Repeating Characters

Given a string ```s```, find the length of the ***longest substring*** ```without``` repeating characters.

 


 




**Example 1**
```bash
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```
**Example 2**
```bash
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3**
```bash
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
### Constraints

- ```0 <= s.length <= 5 * 104```
- ```s consists of English letters, digits, symbols and spaces.```

## Solution

```javascript
var lengthOfLongestSubstring = function(s) {
    const set = new Set();
    let left = 0;
    let maxSubstrLen = 0;

    for(let right = 0; right < s.length; right++) {
        while(set.has(s[right])) {
            set.delete(s[left]);
            left++;
        }
        set.add(s[right]);
        maxSubstrLen = Math.max(maxSubstrLen, right - left + 1);
    }
    return maxSubstrLen;
};
```
