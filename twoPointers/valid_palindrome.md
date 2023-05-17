
##   Valid Palindrome

A phrase is a ```palindrome``` if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string ```s```, return ```true``` if it is a **palindrome**, or ```false``` otherwise.


 




**Example 1**
```bash
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```
**Example 2**
```bash
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Example 3**
```bash
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```
    
### Constraints

- ```1 <= s.length <= 2 * 105```

- ```s consists only of printable ASCII characters.```

## Solution

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        int i = 0;
        int j = s.size() - 1;
        while(i < j) {
            while(i<j && !isalnum(s[i])) {
                i++;
            }
            while(i<j && !isalnum(s[j])) {
                j--;
            }
            if(tolower(s[i])!=tolower(s[j])) {
                return false;
            }
            i++;j--;
        }
        return true;
    }
};
```

```javascript
var isPalindrome = function(s) {
    const sanitized = s.replace(/[^0-9a-z]/gi, '').toLowerCase();
    let i = 0, j = sanitized.length - 1;
    while(i < j) {
        if(sanitized[i] !== sanitized[j]) {
            return false;
        }
        i++;j--;
    }
    return true;
};
```
