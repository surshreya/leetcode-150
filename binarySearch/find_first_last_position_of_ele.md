
## Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in non-decreasing order, find the ```starting``` and ending position of a given target value.

If target is not found in the array, return ```[-1, -1]```.

You must write an algorithm with ```O(log n)``` runtime complexity.

 

**Example 1**
```bash
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2**
```bash
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

**Example 3**
```bash
Input: nums = [], target = 0
Output: [-1,-1]
```


### Constraints
- 0 <= nums.length <= 105
- -109 <= nums[i] <= 109
- nums is a non-decreasing array.
- -109 <= target <= 109

## Solution

```javascript
//**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function(nums, target) {
    const n = nums.length;
    const result = [];
    const findFirst = () => {
        let l=0,h=n-1;
        let result = -1;
        while(l<=h) {
            let mid = Math.floor((l+h)/2);
            if(target === nums[mid]) {
                result = mid;
            }

            if(nums[mid] >= target) {
                h=mid-1;
            } else {
                l=mid+1
            }
        }
        return result;
    }

    const findLast = () => {
        let l=0,h=n-1;
        let result = -1;
        while(l<=h) {
            let mid = Math.floor((l+h)/2);
            if(target === nums[mid]) {
                result = mid;
            }

            if(nums[mid] <= target) {
                l=mid+1;
            } else {
                h=mid-1;
            }
        }

        return result;
    }

    const first = findFirst();
    const last = findLast();
    return [first, last];
};
```
