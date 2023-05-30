
##  Evaluate Division

You are given an array of variable pairs ```equations``` and an array of real numbers ```values```, where ```equations[i] = [Ai, Bi] and values[i] represent the equation Ai / Bi = values[i]```. Each ```Ai``` or ```Bi``` is a string that represents a single variable.

You are also given some ```queries```, where ```queries[j] = [Cj, Dj]``` represents the jth query where you must find the answer for ```Cj / Dj = ?.```

```Return the answers to all queries.``` If a single answer cannot be determined, return ```-1.0```.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.
 


 

**Example 1**
```bash
Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
Explanation: 
Given: a / b = 2.0, b / c = 3.0
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
```

**Example 2**
```bash
Input: equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
Output: [3.75000,0.40000,5.00000,0.20000]
```

**Example 3**
```bash
Input: equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
Output: [0.50000,2.00000,-1.00000,-1.00000]
```

### Constraints
- 1 <= equations.length <= 20
- equations[i].length == 2
- 1 <= Ai.length, Bi.length <= 5
- values.length == equations.length
- 0.0 < values[i] <= 20.0
- 1 <= queries.length <= 20
- queries[i].length == 2
- 1 <= Cj.length, Dj.length <= 5
- Ai, Bi, Cj, Dj consist of lower case English letters and digits.

## Solution

```javascript
const dfs = (c, d, visited, graph) => {
  if (!graph.has(c) || !graph.has(d)) {
    return -1.0;
  }
  
  if (c === d) {
    return 1.0;
  }

  visited.add(c);
  const neighbors = graph.get(c);
  for (let [next, val] of neighbors) {
    if (!visited.has(next)) {
      const res = dfs(next, d, visited, graph);
      if (res !== null) {
        return val * res;
      }
    }
  }

  return null;
};

/**
 * @param {string[][]} equations
 * @param {number[]} values
 * @param {string[][]} queries
 * @return {number[]}
 */
var calcEquation = function(equations, values, queries) {
    const graph = new Map();
    const result = [];
    for(let i=0;i<equations.length;i++) {
        const [a,b] = equations[i];
        if(!graph.has(a)) {
            graph.set(a, new Map());
        }

        if(!graph.has(b)) {
            graph.set(b, new Map());
        }

        graph.get(a).set(b, values[i]);
        graph.get(b).set(a, 1 / values[i]);
    }
    
    for(let [c, d] of queries) {
        if(!graph.has(c) || !graph.has(d)) {
            result.push(-1);
            continue;
        }
        const visited = new Set();
        const val = dfs(c, d, visited, graph);
        result.push(val !== null ? val : -1.0);
    }
    return result;
};
```
