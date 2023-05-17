## Max Points on a Line

Implement `pow(x, n)`, which calculates `x` raised to the power n (i.e., `xn`).

Given an array of points where `points[i] = [xi, yi]` represents a point on the **X-Y** plane, return the `maximum number of points that lie on the same straight line.`

**Example 1**

```bash
Input: points = [[1,1],[2,2],[3,3]]
Output: 3
```

**Example 2**

```bash
Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
```

### Constraints

- 1 <= points.length <= 300
- points[i].length == 2
- -104 <= xi, yi <= 104
- All the points are unique.

## Solution

```javascript
/**
 * @param {number[][]} points
 * @return {number}
 */
var maxPoints = function (points) {
  if (points.length <= 2) {
    return points.length;
  }

  let maxCount = 0;

  for (let i = 0; i < points.length - 1; i++) {
    const slopes = new Map();
    let samePointCount = 1;
    let curMax = 0;

    for (let j = i + 1; j < points.length; j++) {
      const x1 = points[i][0];
      const y1 = points[i][1];
      const x2 = points[j][0];
      const y2 = points[j][1];

      if (x1 === x2 && y1 === y2) {
        samePointCount++;
        continue;
      }

      const slope = x1 - x2 === 0 ? Infinity : (y1 - y2) / (x1 - x2);
      if (!slopes.has(slope)) {
        slopes.set(slope, 1);
      } else {
        slopes.set(slope, slopes.get(slope) + 1);
      }
      curMax = Math.max(curMax, slopes.get(slope));
    }
    curMax += samePointCount;
    maxCount = Math.max(maxCount, curMax);
    console.log(slopes, curMax);
  }

  return maxCount;
};
```
