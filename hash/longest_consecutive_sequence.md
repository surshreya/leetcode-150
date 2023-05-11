## Longest Consecutive Sequence

Given an unsorted array of integers `nums`, return the length of the **_`longest consecutive elements sequence`._**

You must write an algorithm that runs in `O(n)` time.

**Example 1**

```bash
Input: nums = [100,4,200,1,3,2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```

**Example 2**

```bash
Input: nums = [0,3,7,2,5,8,4,6,0,1]
Output: 9
```

### Constraints

- 0 <= nums.length <= 105
- -109 <= nums[i] <= 109

## Solution

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function (nums) {
  const set = new Set();
  const n = nums.length;

  for (let i = 0; i < n; i++) {
    set.add(nums[i]);
  }

  let currSeq = 0,
    maxSeq = 0;
  for (let i = 0; i < nums.length; i++) {
    if (!set.has(nums[i] - 1)) {
      let curr = nums[i];
      let currSeq = 1;
      while (set.has(curr + 1)) {
        curr += 1;
        currSeq += 1;
      }
      maxSeq = Math.max(maxSeq, currSeq);
    }
  }
  return maxSeq;
};
```
