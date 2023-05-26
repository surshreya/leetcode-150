
## Letter Combinations of a Phone Number

Given a string containing digits from ```2-9``` inclusive, ```return all possible letter combinations that the number could represent.``` Return the answer in **any order**.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

 

![1200px-telephone-keypad2svg](https://github.com/surshreya/leetcode-150/assets/118065908/dbc01218-8a0d-467e-b361-98b67628cf67)

 

**Example 1**
```bash
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Example 2**
```bash
Input: digits = ""
Output: []
```

**Example 2**
```bash
Input: digits = "2"
Output: ["a","b","c"]
```

### Constraints
- 0 <= digits.length <= 4
- digits[i] is a digit in the range ['2', '9'].

## Solution

```javascript
/**
 * @param {string} digits
 * @return {string[]}
 */

 const getLetterCombinations = (i, cur, digits, map, result) => {
     if(i === digits.length) {
         result.push(cur);
         return;
     }

     const letters = map[digits[i]];
     for(let k=0;k<letters.length;k++) {
         getLetterCombinations(i+1,`${cur}${letters[k]}`,digits,map,result);
     }
 }

var letterCombinations = function(digits) {
    if(digits.length === 0) return [];

    const letterCombinations = [];
    const map = {
        '2': ['a','b','c'],
        '3': ['d','e','f'],
        '4': ['g','h','i'],
        '5': ['j','k','l'],
        '6': ['m','n','o'],
        '7': ['p','q','r','s'],
        '8': ['t','u','v'],
        '9': ['w','x','y','z']
    }

    getLetterCombinations(0, '', digits, map, letterCombinations);
    return letterCombinations;
};
```
