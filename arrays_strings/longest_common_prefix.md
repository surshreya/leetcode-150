
## Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string ```""```.




**Example 1**
```bash
  Input: strs = ["flower","flow","flight"]
  Output: "fl"
```
**Example 2**
```bash
  Input: strs = ["dog","racecar","car"]
  Output: ""
  Explanation: There is no common prefix among the input strings.
```

    
### Constraints

- ```1 <= strs.length <= 200```

- ```0 <= strs[i].length <= 200```

- ```strs[i] consists of only lowercase English letters.```

## Solution

```javascript
var longestCommonPrefix = function(strs) {
    if(!strs || strs.length === 0) return;

    let idx = 0;
    for(let i=0; i < strs[0].length;i++) {
        let ok = 1;
        for(let j=1; j < strs.length; j++) {
            if(idx > strs[j].length || strs[j][i] !== strs[0][i]) {
                ok = 0;
                break;
            }
        }
        if(ok) {
            idx++;
        } else {
            break;
        }
    }
    return strs[0].substring(0, idx);
};
```
