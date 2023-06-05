
##   Median of Two Sorted Arrays

Given two sorted arrays ```nums1``` and ```nums2``` of size ```m``` and ```n``` respectively, return **the median** of the two sorted arrays.

The overall run time complexity should be ```O(log (m+n)).```

 

**Example 1**
```bash
Input: nums1 = [1,3], nums2 = [2]
Output: 2.00000
Explanation: merged array = [1,2,3] and median is 2.
```

**Example 2**
```bash
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.50000
Explanation: merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
```

### Constraints

- ```nums1.length == m```
- ```nums2.length == n```
- ```0 <= m <= 1000```
- ```0 <= n <= 1000```
- ```1 <= m + n <= 2000```
- ```-106 <= nums1[i], nums2[i] <= 106```

## Solution
```javascript
const median = (nums1, nums2, n, m) => {
    if(n>m) {
        return median(nums2, nums1, m, n);
    }

    let low = 0, high = n, medianPos = Math.floor((m+n+1)/2);

    while(low<=high) {
        let c1 = (low+high) >> 1;
        let c2 = medianPos - c1;

        let l1 = c1 === 0 ?  Number.MIN_SAFE_INTEGER : nums1[c1 - 1];
        let l2 = c2 === 0 ?  Number.MIN_SAFE_INTEGER : nums2[c2 - 1];
        let r1 = c1 === n ?  Number.MAX_SAFE_INTEGER : nums1[c1];
        let r2 = c2 === m ?  Number.MAX_SAFE_INTEGER : nums2[c2];

        if(l1 <= r2 && l2 <= r1) {
            if((m+n)%2 !==0) {
                return Math.max(l1,l2);
            } else {
                return (Math.max(l1,l2) + Math.min(r1,r2))/2.0;
            } 
        } else if(l1>l2) {
            high = c1-1;
        } else {
            low = c1+1;
        }
    }
    return 0.0;
}
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
    let n = nums1.length;
    let m = nums2.length;
    return median(nums1, nums2, n, m)
};
```

