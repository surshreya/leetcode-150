
##   Best Time to Buy and Sell Stock III

You are given an array ```prices``` where ```prices[i] is the price of a given stock on the ith day.```

Find the maximum profit you can achieve. You may complete **at most two transactions**.

**Note:** You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).
 
 

 

**Example 1**
```bash
Input: prices = [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

**Example 2**
```bash
Input: prices = [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3**
```bash
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

### Constraints

- 1 <= prices.length <= 105
- 0 <= prices[i] <= 105


## Solution
```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    const n = prices.length;
    let ahead = Array.from({ length: 2 }, () => Array(3).fill(0));
    let cur = Array.from({ length: 2 }, () => Array(3).fill(0));
    
    for (let ind = n - 1; ind >= 0; ind--) {
        for (let buy = 0; buy <= 1; buy++) {
            for (let cap = 1; cap <= 2; cap++) {
                if (buy === 0) {
                // We can buy the stock
                cur[buy][cap] = Math.max(0 + ahead[0][cap], -prices[ind] + ahead[1][cap]);
                }

                if (buy === 1) {
                    // We can sell the stock
                    cur[buy][cap] = Math.max(0 + ahead[1][cap], prices[ind] + ahead[0][cap - 1]);
                }
            }
        }
        ahead = [...cur];
    }
    return ahead[0][2];

};
```

