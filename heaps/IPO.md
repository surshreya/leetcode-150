
##   IPO

Suppose LeetCode will start its **IPO** soon. In order to sell a good price of its shares to Venture Capital, LeetCode would like to work on some projects to increase its capital before the IPO. Since it has limited resources, it can only finish at most k distinct projects before the IPO. Help LeetCode design the best way to maximize its total capital after finishing at most k distinct projects.

You are given n projects where the ```ith``` project has a pure profit ```profits[i]``` and a ```minimum capital of capital[i]``` is needed to start it.

Initially, you have w capital. When you finish a project, you will obtain its pure profit and the profit will be added to your total capital.

```Pick a list of at most k distinct projects from given projects to maximize your final capital, and return the final maximized capital.```

The answer is guaranteed to fit in a 32-bit signed integer.

 

 

**Example 1**
```bash
Input: k = 2, w = 0, profits = [1,2,3], capital = [0,1,1]
Output: 4
Explanation: Since your initial capital is 0, you can only start the project indexed 0.
After finishing it you will obtain profit 1 and your capital becomes 1.
With capital 1, you can either start the project indexed 1 or the project indexed 2.
Since you can choose at most 2 projects, you need to finish the project indexed 2 to get the maximum capital.
Therefore, output the final maximized capital, which is 0 + 1 + 3 = 4.
```

**Example 2**
```bash
Input: k = 3, w = 0, profits = [1,2,3], capital = [0,1,2]
Output: 6
```

### Constraints

- ```1 <= k <= 105```
- ```0 <= w <= 109```
-``` n == profits.length```
-``` n == capital.length```
- ```1 <= n <= 105```
- ```0 <= profits[i] <= 104```
- ```0 <= capital[i] <= 109```

## Solution
```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
  }

  insert(value) {
    this.heap.push(value);
    this.heapifyUp(this.heap.length - 1);
  }

  extractMax() {
    const max = this.heap[0];
    const last = this.heap.pop();
    if (this.heap.length > 0) {
      this.heap[0] = last;
      this.heapifyDown(0);
    }
    return max;
  }

  heapifyUp(index) {
    const parentIndex = Math.floor((index - 1) / 2);
    if (parentIndex >= 0 && this.heap[parentIndex][0] < this.heap[index][0]) {
      [this.heap[parentIndex], this.heap[index]] = [this.heap[index], this.heap[parentIndex]];
      this.heapifyUp(parentIndex);
    }
  }

  heapifyDown(index) {
    const leftChildIndex = 2 * index + 1;
    const rightChildIndex = 2 * index + 2;
    let largestIndex = index;

    if (
      leftChildIndex < this.heap.length &&
      this.heap[leftChildIndex][0] > this.heap[largestIndex][0]
    ) {
      largestIndex = leftChildIndex;
    }

    if (
      rightChildIndex < this.heap.length &&
      this.heap[rightChildIndex][0] > this.heap[largestIndex][0]
    ) {
      largestIndex = rightChildIndex;
    }

    if (largestIndex !== index) {
      [this.heap[index], this.heap[largestIndex]] = [this.heap[largestIndex], this.heap[index]];
      this.heapifyDown(largestIndex);
    }
  }

  isEmpty() {
    return this.heap.length === 0;
  }
}

/**
 * @param {number} k
 * @param {number} w
 * @param {number[]} profits
 * @param {number[]} capital
 * @return {number}
 */
var findMaximizedCapital = function(k, w, profits, capital) {
    const n = profits.length;
    const projects = [];
    const maxHeap = new MaxHeap();

    for(let i=0;i<n;i++) {
        projects.push([profits[i], capital[i]]);
    }

    projects.sort((a,b)=>a[1]-b[1]);

    let availCapital = w;
    let curIdx = 0;
    for(let i=0;i<k;i++) {
      while(curIdx < n && projects[curIdx][1] <= availCapital) {
        maxHeap.insert(projects[curIdx]);
        curIdx++;
      }

      if(maxHeap.isEmpty()) break;
      availCapital+=maxHeap.extractMax()[0];
    }

    return availCapital;
};
```

