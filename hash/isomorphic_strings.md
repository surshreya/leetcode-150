## Isomorphic Strings

Given two strings s and t, determine if they are isomorphic.

Two strings s and t are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.

**Example 1**

```bash
Input: s = "egg", t = "add"
Output: true
```

**Example 2**

```bash
Input: s = "foo", t = "bar"
Output: false
```

**Example 3**

```bash
Input: s = "paper", t = "title"
Output: true
```

### Constraints

- `1 <= s.length <= 5 * 104`
- `t.length == s.length`
- `s and t consist of any valid ascii character.`

## Solution

```javascript
var isIsomorphic = function (s, t) {
  if (s.length !== t.length) return false;

  let sMap = {};
  let tMap = {};

  for (let i = 0; i < s.length; i++) {
    let sChar = s[i];
    let tChar = t[i];

    if (!sMap[sChar]) sMap[sChar] = tChar;
    if (!tMap[tChar]) tMap[tChar] = sChar;

    if (sChar !== tMap[tChar] || tChar !== sMap[sChar]) {
      return false;
    }
  }

  return true;
};
```
