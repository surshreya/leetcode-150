## Permutations

Given an array `nums` of distinct integers, return **_`all the possible permutations`_**. You can return the answer in **any order**.

**Example 1**

```bash
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**Example 2**

```bash
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

**Example 2**

```bash
Input: nums = [1]
Output: [[1]]
```

### Constraints

- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- All the integers of nums are unique.

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
const getPermutation = (result, nums, i) => {
  if (i === nums.length) {
    result.push([...nums]);
    return;
  }

  for (let k = i; k < nums.length; k++) {
    [nums[i], nums[k]] = [nums[k], nums[i]];
    getPermutation(result, nums, i + 1);
    [nums[i], nums[k]] = [nums[k], nums[i]];
  }
};

var permute = function (nums) {
  const permutations = [];
  getPermutation(permutations, nums, 0);
  return permutations;
};
```
