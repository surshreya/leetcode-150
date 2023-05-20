## Reverse Words in a String

Given an input string `s`, reverse the order of the **_words_**.

A **word** is defined as a sequence of non-space characters. The words in s will be separated by `at least one space`.

**_`Return a string of the words in reverse order concatenated by a single space.`_**

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1**

```bash
Input: s = "the sky is blue"
Output: "blue is sky the"
```

**Example 2**

```bash
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3**

```bash
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

### Constraints

- 1 <= s.length <= 104
- s contains English letters (upper-case and lower-case), digits, and spaces ' '.
- There is at least one word in s.

**Follow-up:** If the string data type is mutable in your language, can you solve it **_in-place_** with `O(1)` extra space?

## Solution

**_C++_**

```cpp
class Solution {
public:
    string reverseWords(string s) {
        int l = 0;
        int r = s.length() - 1;

        string temp = "";
        string result = "";

        while(l <= r) {
            char ch = s[l];
            if(ch != ' ') {
                temp += ch;
            } else {
                if(result != "") {
                    result = temp + " " + result;
                } else {
                    result = temp;
                }
                temp = "";
            }
            l++;
        }

        if (temp!="") {
            if (result!="") {
                result = temp + " " + result;
            } else {
                result = temp;
            }
        }
        return result;
    }
};
```

**_Javascript_**

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function (s) {
  const result = s
    .trim()
    .split(" ")
    .filter((ele) => ele !== "")
    .reverse()
    .join(" ");
  return result;
};
```
