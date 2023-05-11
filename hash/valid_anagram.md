## Valid Anagram

Given two strings `s` and `t`, return `true` if t is an anagram of s, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly `once`.

**Example 1**

```bash
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2**

```bash
Input: s = "rat", t = "car"
Output: false
```

### Constraints

- `1 <= s.length, t.length <= 5 * 104`
- `s and t consist of lowercase English letters.`

## Solution

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.length() != t.length()) {
            return false;
        }

        vector<int> ch(256);
        for (const char c : s) {
           ++ch[c];
        }


        for(const char c : t) {
            ch[c]--;
            if(ch[c] < 0) {
                return false;
            }
        }
        return true;
    }
};
```

```javascript
var isAnagram = function (s, t) {
  if (s.length != t.length) return false;

  let mp = new Map();
  for (let i = 0; i < s.length; i++) {
    if (mp.has(s[i])) {
      mp.set(s[i], mp.get(s[i]) + 1);
    } else {
      mp.set(s[i], 1);
    }
  }

  for (let i = 0; i < t.length; i++) {
    if (mp.has(t[i])) {
      mp.set(t[i], mp.get(t[i]) - 1);
    } else {
      return false;
    }
  }

  let keys = mp.keys();
  for (let key of keys) {
    if (mp.get(key) !== 0) {
      return false;
    }
  }
  return true;
};
```
