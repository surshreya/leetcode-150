## Length of Last Word

Given a string `s` consisting of words and spaces, **_`return the length of the last word in the string.`_**

A word is a **maximal** substring consisting of non-space characters only.

**Example 1**

```bash
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.
```

**Example 2**

```bash
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.
```

**Example 3**

```bash
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```

### Constraints

- 1 <= s.length <= 104
- s consists of only English letters and spaces ' '.
- There will be at least one word in s.

## Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function (s) {
  const words = s.trim().split(" ");
  return words[words.length - 1].length;
};
```
