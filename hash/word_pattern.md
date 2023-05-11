## Word Pattern

Given a `pattern` and a string `s`, find if `s follows the same pattern.`

Here follow means a full match, such that there is a **_`bijection`_** between a letter in pattern and a non-empty word in s.

**Example 1**

```bash
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```

**Example 2**

```bash
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```

**Example 2**

```bash
Input: pattern = "abba", s = "dog cat cat dog"
Output: true
```

### Constraints

- 1 <= pattern.length <= 300
- pattern contains only lower-case English letters.
- 1 <= s.length <= 3000
- s contains only lowercase English letters and spaces ' '.
- s does not contain any leading or trailing spaces.
- All the words in s are separated by a single space.

## Solution

```javascript
/**
 * @param {string} pattern
 * @param {string} s
 * @return {boolean}
 */
var wordPattern = function (pattern, s) {
  const words = s.split(" ");
  const wordMap = new Map();
  const patternMap = new Map();

  if (words.length !== pattern.length) return false;

  for (let i = 0; i < words.length; i++) {
    const letter = pattern[i];
    const word = words[i];
    if (
      (patternMap.has(letter) && patternMap.get(letter) !== word) ||
      (wordMap.has(word) && wordMap.get(word) !== letter)
    ) {
      return false;
    } else {
      patternMap.set(letter, word);
      wordMap.set(word, letter);
    }
  }

  return true;
};
```
