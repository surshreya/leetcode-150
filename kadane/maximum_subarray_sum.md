## Maximum Subarray

Given an integer array `nums`, find the
subarray with the **largest sum**, and return its sum.

**Example 1**

```bash
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
```

**Example 2**

```bash
Input: nums = [1]
Output: 1
Explanation: The subarray [1] has the largest sum 1.
```

**Example 3**

```bash
Input: nums = [5,4,-1,7,8]
Output: 23
Explanation: The subarray [5,4,-1,7,8] has the largest sum 23. 15 at t=120ms. The time limit is never reached.
```

### Constraints

- 1 <= nums.length <= 105
- -104 <= nums[i] <= 104

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
  let max = -Infinity;
  let sum = 0;

  for (let i = 0; i < nums.length; i++) {
    sum += nums[i];
    if (sum > max) {
      max = sum;
    }

    if (sum < 0) {
      sum = 0;
    }
  }
  return max;
};
```
