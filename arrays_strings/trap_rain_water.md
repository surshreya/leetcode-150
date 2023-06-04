
##  Trapping Rain Water

Given ```n``` non-negative integers representing an elevation map where the width of each bar is ```1```, compute ```how much water it can trap after raining.```
 
![rainwatertrap](https://github.com/surshreya/leetcode-150/assets/118065908/ff45c7e8-5201-4766-928f-b3555116f6d9)

**Example 1**
```bash
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
```

**Example 2**
```bash
Input: height = [4,2,0,3,2,5]
Output: 9
```

### Constraints

- ```n == height.length```
- ```1 <= n <= 2 * 104```
- ```0 <= height[i] <= 105```
 
## Solution
***```Solution 1```***
```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function(height) {
    const n = height.length;
    const prefix = [];
    const suffix = [];

    prefix[0] = height[0];
    for(let i=1;i<n;i++) {
        prefix[i] = Math.max(prefix[i-1], height[i]);
    }
    suffix[n-1] = height[n-1];
    for (let i=n-2;i>=0;i--) {
        suffix[i] = Math.max(suffix[i+1], height[i]);
    }

    let waterTrapped = 0;
    for (let i=0;i<n;i++) {
        waterTrapped += Math.min(prefix[i], suffix[i]) - height[i];
    }
    return waterTrapped;
};
```

***```Solution 2```***
```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function(height) {
    const n = height.length;
    let left = 0, right = n-1;
    let water = 0;
    let maxLeft = 0, maxRight = 0;
    while(left <= right) {
        if(height[left] <= height[right]) {
            if(height[left] >= maxLeft) {
                maxLeft = height[left];
            } else {
                water += maxLeft - height[left];
            }
            left++;
        } else {
            if(height[right] >= maxRight) {
                maxRight = height[right];
            } else {
                water += maxRight - height[right];
            }
            right--;
        }
    }
    return water;
};
```
