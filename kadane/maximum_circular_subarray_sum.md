## Maximum Sum Circular Subarray

Given a circular integer array `nums` of length `n`, return the **`maximum possible sum of a non-empty subarray of nums.`**

A **circular** array means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i] is nums[(i + 1) % n]` and the previous element of `nums[i] is nums[(i - 1 + n) % n].`

A subarray may only include each element of the fixed buffer nums at most once. `Formally, for a subarray nums[i], nums[i + 1], ..., nums[j], there does not exist i <= k1, k2 <= j with k1 % n == k2 % n.`

**Example 1**

```bash
Input: nums = [1,-2,3,-2]
Output: 3
Explanation: Subarray [3] has maximum sum 3.
```

**Example 2**

```bash
Input: nums = [5,-3,5]
Output: 10
Explanation: Subarray [5,5] has maximum sum 5 + 5 = 10.
```

**Example 3**

```bash
Input: nums = [-3,-2,-3]
Output: -2
Explanation: Subarray [-2] has maximum sum -2.
```

### Constraints

- n == nums.length
- 1 <= n <= 3 \* 104
- -3 _ 104 <= nums[i] <= 3 _ 104

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubarraySumCircular = function (nums) {
  let sum = nums.reduce((acc, ele) => acc + ele, 0);
  let currMax = nums[0],
    max = nums[0],
    currMin = nums[0],
    min = nums[0];

  for (let i = 1; i < nums.length; i++) {
    currMax = Math.max(currMax + nums[i], nums[i]);
    max = Math.max(max, currMax);

    currMin = Math.min(currMin + nums[i], nums[i]);
    min = Math.min(min, currMin);
  }

  if (max < 0) return max;

  return Math.max(max, sum - min);
};
```
