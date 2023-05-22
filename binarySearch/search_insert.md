## Search Insert Position

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

**Example 1**

```bash
Input: nums = [1,3,5,6], target = 5
Output: 2
```

**Example 2**

```bash
Input: nums = [1,3,5,6], target = 2
Output: 1
```

**Example 3**

```bash
Input: nums = [1,3,5,6], target = 7
Output: 4
```

### Constraints

- 1 <= nums.length <= 104
- -104 <= nums[i] <= 104
- nums contains distinct values sorted in ascending order.
- -104 <= target <= 104

## Solution

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function (nums, target) {
  let l = 0,
    r = nums.length - 1;
  let mid, res;
  while (l <= r) {
    mid = Math.floor((l + r) / 2);
    if (nums[mid] === target) {
      return mid;
    } else if (nums[mid] < target) {
      l = mid + 1;
      res = mid + 1;
    } else {
      res = mid;
      r = mid - 1;
    }
  }
  return res;
};
```
