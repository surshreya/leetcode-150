
##  Convert Sorted Array to Binary Search Tree

Given an integer array nums where the elements are sorted in **ascending order**, convert it to a **height-balanced
 binary search tree**.



 




**Example 1**
```bash
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:
```
**Example 2**
```bash
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.
```
    
### Constraints

- ```1 <= nums.length <= 104```
- ```-104 <= nums[i] <= 104```
- ```nums is sorted in a strictly increasing order.```


## Solution

```javascript
 class Node {
     constructor(val) {
         this.val = val;
         this.left = null;
         this.right = null
     }
 }

 const buildTree = (nums, l, r) => {
     if(r<l) return null;

     let mid = Math.floor((l+r)/2);
     const root = new Node(nums[mid]);
     root.left = buildTree(nums, l, mid-1);
     root.right = buildTree(nums, mid+1, r);
     return root;
 }

var sortedArrayToBST = function(nums) {
    if(!nums || nums.length === 0) return NULL;
    return buildTree(nums, 0, nums.length-1);
};
```
