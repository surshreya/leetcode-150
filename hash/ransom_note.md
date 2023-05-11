## Ransom Note

Given two strings `ransomNote` and `magazine`, return `true if ransomNote can be constructed by using the letters from magazine` and `false` otherwise.

Each letter in magazine can only be used once in ransomNote.

**Example 1**

```bash
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2**

```bash
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2**

```bash
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

### Constraints

- `1 <= ransomNote.length, magazine.length <= 105`
- `ransomNote and magazine consist of lowercase English letters.`

## Solution

```javascript
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function (ransomNote, magazine) {
  const mp = new Map();
  for (let i = 0; i < magazine.length; i++) {
    if (mp.has(magazine[i])) {
      mp.set(magazine[i], mp.get(magazine[i]) + 1);
    } else {
      mp.set(magazine[i], 1);
    }
  }

  for (let i = 0; i < ransomNote.length; i++) {
    if (!mp.has(ransomNote[i]) || mp.get(ransomNote[i]) === 0) {
      return false;
    }
    mp.set(ransomNote[i], mp.get(ransomNote[i]) - 1);
  }

  return true;
};
```
