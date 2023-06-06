
##   Edit Distance

Given two strings ```word1``` and ```word2```, ```return the minimum number of operations required to convert word1 to word2.```

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character
 
 

 

**Example 1**
```bash
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
```

**Example 2**
```bash
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

### Constraints

- 0 <= word1.length, word2.length <= 500
- word1 and word2 consist of lowercase English letters.


## Solution
```javascript
/**
 * @param {string} word1
 * @param {string} word2
 * @return {number}
 */
var minDistance = function(word1, word2) {
    const n = word1.length;
    const m = word2.length;

    const prev = new Array(m + 1).fill(0);
    const cur = new Array(m + 1).fill(0);

    for (let j = 0; j <= m; j++) {
        prev[j] = j;
    }
    
    for (let i = 1; i <= n; i++) {
        cur[0] = i;
        for (let j = 1; j <= m; j++) {
            if (word1[i - 1] === word2[j - 1])
                cur[j] = 0 + prev[j - 1];
            else
                cur[j] = 1 + Math.min(prev[j - 1], Math.min(prev[j], cur[j - 1]));
        }
        prev.splice(0, prev.length, ...cur);
    }
    return prev[m];
};
```

