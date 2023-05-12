## Merge Intervals

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and `return an array of the non-overlapping intervals that cover all the intervals in the input.`

**Example 1**

```bash
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
```

**Example 2**

```bash
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

### Constraints

- 1 <= intervals.length <= 104
- intervals[i].length == 2
- 0 <= starti <= endi <= 104

## Solution

```javascript
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function (intervals) {
  intervals.sort((a, b) => a[0] - b[0]);
  const merged = [];
  for (let i = 0; i < intervals.length; i++) {
    if (merged.length === 0 || merged[merged.length - 1][1] < intervals[i][0]) {
      let v = [intervals[i][0], intervals[i][1]];
      merged.push(v);
    } else {
      merged[merged.length - 1][1] = Math.max(
        merged[merged.length - 1][1],
        intervals[i][1]
      );
    }
  }

  return merged;
};
```
