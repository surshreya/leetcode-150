
##  Find the Index of the First Occurrence in a String

Given two strings needle and haystack, return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.




**Example 1**
```bash
Input: haystack = "sadbutsad", needle = "sad"
Output: 0
Explanation: "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
```
**Example 2**
```bash
Input: haystack = "leetcode", needle = "leeto"
Output: -1
Explanation: "leeto" did not occur in "leetcode", so we return -1.
```
    
### Constraints

- ```1 <= haystack.length, needle.length <= 104```

- ```haystack and needle consist of only lowercase English characters.```

## Solution

```cpp
class Solution {
public:
    int strStr(string haystack, string needle) {
        int len = needle.size();
        int n = haystack.size();
        if(n < len ) {
            return -1;
        }
        for(int i=0;i<=n-len;i++) {
            if(string(haystack.begin()+i, haystack.begin()+i+len) == needle) {
                return i;
            }
        }
        return -1;
    }
};
```

```javascript
var strStr = function(haystack, needle) {
    return haystack.indexOf(needle) ?? -1;
};
```
