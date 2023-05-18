
##    Majority Element

Given an array ```nums``` of size ```n```, return the ```majority element```.

The majority element is the element that appears more than ```⌊n / 2⌋ times```. You may assume that the majority element always exists in the array.



 


 




**Example 1**
```bash
Input: nums = [3,2,3]
Output: 3
```
**Example 2**
```bash
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```

### Constraints

- ```n == nums.length```
- ```1 <= n <= 5 * 104```
- ```-109 <= nums[i] <= 109```
## Solution

***Moore Voting Algorithm***
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int count = 0;
        int candidate = 0;
        for(int num:nums) {
            if(count == 0) {
                candidate = num;
            }
            if(num == candidate) {
                count = count + 1;
            } else {
                count = count - 1;
            }
        }
        return candidate;
    }
};
```
***Map***
```javascript
var majorityElement = function(nums) {
     const mp = new Map();
     const majorityNum = Math.floor(nums.length/2);
     for(let i = 0; i < nums.length; i++) {
         if(mp.has(nums[i])) {
             mp.set(nums[i], mp.get(nums[i])+1);
         } else {
             mp.set(nums[i], 1);
         }
     }

     for(let [key, val] of mp) {
         if(val > majorityNum) {
             return key;
         }
     }

    return -1;
};
```
