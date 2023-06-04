
##   Kth Largest Element in an Array

Given an integer array ```nums``` and an integer ```k```, return the **kth largest element** in the array.

Note that it is the kth largest element in the sorted order, not the kth distinct element.

You must solve it in ***O(n)*** time complexity.

**Example 1**
```bash
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

**Example 2**
```bash
Input: nums = [1], k = 1
Output: [1]
```

### Constraints

- ```1 <= nums.length <= 105```
- ```-104 <= nums[i] <= 104```

## Solution

***``` Max Heap ```***
```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function(nums, k) {
    const pq = new MaxPriorityQueue({
        comparator: (a,b) => b-a
    });

    nums.forEach(num => {
        pq.enqueue(num);
    })

    return pq.toArray()[k-1].element;
};
```

***``` Quick Sort ```***
```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */

 const swap = (arr, i, j) => {
     let temp = arr[i];
     arr[i] = arr[j];
     arr[j] = temp;
 }

 const partition = (arr, l, r) => {
     const pivotIdx = r;
     let i=l;
     for(let j = l; j < r; j++) {
         if(arr[j] > arr[pivotIdx]) {
             swap(arr, i, j);
             i++;
         }
     }
     swap(arr, i, pivotIdx);
     return i;
 }

 const getKthLargest = (arr, l, r, k) => {
     const pivotIdx = partition(arr,l,r);
     if(pivotIdx === k-1) {
        return arr[pivotIdx];
     } else if(pivotIdx < k-1) {
        return getKthLargest(arr, pivotIdx+1, r, k);
     } else {
        return getKthLargest(arr, l, pivotIdx-1, k);
     }
 }
var findKthLargest = function(nums, k) {
    return getKthLargest(nums, 0, nums.length - 1, k);
};
```
