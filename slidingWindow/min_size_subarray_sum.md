## Minimum Size Subarray Sum

Given an array of positive integers `nums` and a positive integer `target`, return the **minimal length of a subarray** whose sum is `greater than or equal to target`. If there is no such subarray, return `0` instead.

**Example 1**

```bash
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```

**Example 2**

```bash
Input: target = 4, nums = [1,4,4]
Output: 1
```

**Example 3**

```bash
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```

### Constraints

- 1 <= target <= 109
- 1 <= nums.length <= 105
- 1 <= nums[i] <= 104

## Solution

```javascript
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function (target, nums) {
  let minLength = Infinity;
  let l = 0;
  let windowSum = 0;

  for (let r = 0; r < nums.length; r++) {
    windowSum += nums[r];

    while (windowSum >= target) {
      minLength = Math.min(minLength, r - l + 1);
      windowSum -= nums[l];
      l++;
    }
  }

  return minLength === Infinity ? 0 : minLength;
};
```
