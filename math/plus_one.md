
##  Plus One

You are given a large integer represented as an integer array digits, where each digits[i] is the ith digit of the integer. The digits are ordered from most significant to least significant in left-to-right order. The large integer does not contain any leading 0's.

Increment the large integer by one and return the resulting array of digits.

 




**Example 1**
```bash
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Incrementing by one gives 123 + 1 = 124.
Thus, the result should be [1,2,4].
```
**Example 2**
```bash
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
Incrementing by one gives 4321 + 1 = 4322.
Thus, the result should be [4,3,2,2]..
```

**Example 3**
```bash
Input: digits = [9]
Output: [1,0]
Explanation: The array represents the integer 9.
Incrementing by one gives 9 + 1 = 10.
Thus, the result should be [1,0].
```
    
### Constraints

- ```1 <= digits.length <= 100```

- ```0 <= digits[i] <= 9```

- ```digits does not contain any leading 0's.```

## Solution

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int len = digits.size() - 1;
        while(len>=0 && digits[len] == 9) {
            len --;
        }

        if(len == -1) {
            vector<int> result(digits.size(), 0);
            result.insert(result.begin(), 1);
            return result;
        }

        vector<int> result(digits.size(), 0);
        result[len] = digits[len]+1;
        for(int j=0;j<len;j++) {
            result[j]=digits[j];
        }        
        return result;
    }
};
```

```javascript
var plusOne = function(digits) {
    const sum = BigInt(digits.reverse()
    .reduce((acc, cur, i) =>
        BigInt(acc) + BigInt(cur)*BigInt(10)**BigInt(i)
    , 0)) + BigInt(1);

    return Array.from(String(sum), Number);
};
```
