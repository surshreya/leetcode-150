## Integer to Roman

Roman numerals are represented by seven different symbols: **`I, V, X, L, C, D and M.`**

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

- I can be placed before V (5) and X (10) to make 4 and 9.
- X can be placed before L (50) and C (100) to make 40 and 90.
- C can be placed before D (500) and M (1000) to make 400 and 900.

**_`Given an integer, convert it to a roman numeral.`_**

**Example 1**

```bash
Input: num = 3
Output: "III"
Explanation: 3 is represented as 3 ones.
```

**Example 2**

```bash
Input: num = 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

**Example 3**

```bash
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

### Constraints

- 1 <= num <= 3999

## Solution

```javascript
/**
 * @param {number} num
 * @return {string}
 */
var intToRoman = function (num) {
  const romanNumerals = [
    { value: 1000, symbol: "M" },
    { value: 900, symbol: "CM" },
    { value: 500, symbol: "D" },
    { value: 400, symbol: "CD" },
    { value: 100, symbol: "C" },
    { value: 90, symbol: "XC" },
    { value: 50, symbol: "L" },
    { value: 40, symbol: "XL" },
    { value: 10, symbol: "X" },
    { value: 9, symbol: "IX" },
    { value: 5, symbol: "V" },
    { value: 4, symbol: "IV" },
    { value: 1, symbol: "I" },
  ];
  let result = "";
  for (let i = 0; i < romanNumerals.length; i++) {
    const { value, symbol } = romanNumerals[i];
    while (num >= value) {
      result += symbol;
      num -= value;
    }

    if (num === 0) break;
  }
  return result;
};
```
