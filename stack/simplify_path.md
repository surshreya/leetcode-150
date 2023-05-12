## Simplify Path

Given a string `path`, which is an **absolute** path (starting with a slash `'/'`) to a file or directory in a Unix-style file system, convert it to the simplified **canonical path**.

In a Unix-style file system, a period `'.'` refers to the current directory, a double period `'..'` refers to the directory up a level, and any multiple consecutive slashes (i.e. `'//'`) are treated as a single slash `'/'`. For this problem, any other format of periods such as `'...'` are treated as file/directory names.

The **canonical** path should have the following format:

- The path starts with a single slash `'/'`.
- Any two directories are separated by a single slash `'/'`.
- The path does not end with a trailing `'/'`.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period '.' or double period '..')

Return the **simplified canonical path.**

**Example 1**

```bash
Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].
```

**Example 2**

```bash
Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

**Example 2**

```bash
Input: path = "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
```

**Example 3**

```bash
Input: path = "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

### Constraints

- 1 <= path.length <= 3000
- path consists of English letters, digits, period '.', slash '/' or '\_'.
- path is a valid absolute Unix path.

## Solution

```javascript
/**
 * @param {string} path
 * @return {string}
 */
var simplifyPath = function (path) {
  const stack = [];
  let simplifiedPath = "";
  const pathComponents = path.split("/");

  for (let i = 0; i < pathComponents.length; i++) {
    if (pathComponents[i] === "" || pathComponents[i] === ".") {
      continue;
    } else if (pathComponents[i] === "..") {
      if (stack.length) {
        stack.pop();
      }
    } else {
      stack.push(pathComponents[i]);
    }
  }

  if (stack.length === 0) {
    return "/";
  } else {
    while (stack.length !== 0) {
      simplifiedPath = "/" + stack.pop() + simplifiedPath;
    }
  }
  return simplifiedPath;
};
```
