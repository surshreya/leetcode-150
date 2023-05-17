
##  Sqrt(x)

Given a non-negative integer x, return the square root of x rounded down to the nearest integer. The returned integer should be non-negative as well.

**You must not use any built-in exponent function or operator.**

For example, do not use pow(x, 0.5) in c++ or x ** 0.5 in python.

 




**Example 1**
```bash
Input: x = 4
Output: 2
Explanation: The square root of 4 is 2, so we return 2.
```
**Example 2**
```bash
Input: x = 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since we round it down to the nearest integer, 2 is returned.
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

- ```0 <= x <= 231 - 1```

## Solution

```javascript
var mySqrt = function(x) {
    if(x <= 1) return x;
    let l = 0, r = x;
    let mid;

    while((r-l) > 1) {
        mid = (r-l)/2+l;
        if(mid*mid === x) return mid;
        else if(mid*mid>x) r = mid;
        else if(mid*mid<x) l = mid 
    }
    return l;
};
```
