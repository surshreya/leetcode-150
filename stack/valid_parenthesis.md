## Valid Parentheses

Given a string s containing just the characters `'(', ')', '{', '}', '[' and ']'`, determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.

**Example 1**

```bash
  Input: s = "()"
  Output: true
```

**Example 2**

```bash
  Input: s = "()[]{}"
  Output: true
```

**Example 3**

```bash
  Input: s = "(]"
  Output: false
```

### Constraints

- `1 <= s.length <= 104`

- `s consists of parentheses only '()[]{}'.`

## Solution

```javascript
var isValid = function (s) {
  if (!s || s.length === 0) return;

  const stack = [];
  for (const c of s) {
    if (c === "(" || c === "{" || c === "[") {
      stack.push(c);
    } else if (stack.length && c === ")" && stack[stack.length - 1] === "(") {
      stack.pop();
    } else if (stack.length && c === "}" && stack[stack.length - 1] === "{") {
      stack.pop();
    } else if (stack.length && c === "]" && stack[stack.length - 1] === "[") {
      stack.pop();
    } else {
      return false;
    }
  }

  return stack.length === 0 ? true : false;
};
```
