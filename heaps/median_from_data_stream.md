
##   Find Median from Data Stream
The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

- For example, for ```arr = [2,3,4]```, the median is ```3```.
- For example, for``` arr = [2,3],``` the median is ```(2 + 3) / 2 = 2.5.```

Implement the MedianFinder class:

- ```MedianFinder()``` initializes the MedianFinder object.
- ```void addNum(int num)``` adds the integer num from the data stream to the data structure.
- ```double findMedian()``` returns the median of all elements so far. Answers within 10-5 of the actual answer will be accepted.
 
 

 

**Example 1**
```bash
Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
```

### Constraints

- ```-105 <= num <= 105```
- ```There will be at least one element in the data structure before calling findMedian.```
- ```At most 5 * 104 calls will be made to addNum and findMedian.```

**Follow up:**

- If all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?
- If 99% of all integer numbers from the stream are in the range [0, 100], how would you optimize your solution?

## Solution
```javascript
const Heap = (compare) => {
  const list = [];
  const parent = index => Math.floor((index - 1) / 2);
  const left = index => 2 * index + 1;
  const right = index => 2 * index + 2;
  const swap = (a, b) => {
    const temp = list[a];
    list[a] = list[b];
    list[b] = temp;
  }
  const insert = (x) => {
    list.push(x);
    let currentIndex = list.length - 1;
    let parentIndex = parent(currentIndex);
    while (compare(list[parentIndex], list[currentIndex]) > 0) {
      swap(parentIndex, currentIndex);
      currentIndex = parentIndex;
      parentIndex = parent(parentIndex);
    }
  }
  const size = () => list.length;
  const top = () => list[0];
  const sink = (index) => {
    let currentIndex = index;
    const leftIndex = left(index);
    const rightIndex = right(index);
    if (compare(list[currentIndex], list[leftIndex]) > 0) {
      currentIndex = leftIndex;
    }
    if (compare(list[currentIndex], list[rightIndex]) > 0) {
      currentIndex = rightIndex;
    }
    if (currentIndex !== index) {
      swap(index, currentIndex);
      sink(currentIndex);
    }
  }
  const extract = () => {
    swap(0, list.length - 1);
    const result = list.pop();
    sink(0);
    return result;
  }
  return {
    list,
    size,
    top,
    insert,
    extract,
  }
}

var MedianFinder = function() {
  this.maxHeap = Heap((a, b) => b - a);
  this.minHeap = Heap((a, b) => a - b);
  this.size = 0;
};

/** 
 * @param {number} num
 * @return {void}
 */
MedianFinder.prototype.addNum = function(num) {
  this.size += 1;
  const min = this.minHeap.top();
  if (num > min) {
    this.minHeap.insert(num);
    while (this.minHeap.size() > this.maxHeap.size()) { // balance Heaps
      this.maxHeap.insert(this.minHeap.extract());
    }
  } else {
    this.maxHeap.insert(num);
    while (this.maxHeap.size() > this.minHeap.size() + 1) { // balance Heaps
      this.minHeap.insert(this.maxHeap.extract());
    }
  }
};

/**
 * @return {number}
 */
MedianFinder.prototype.findMedian = function() {
  if (this.size > 0) {
    if (this.size % 2 === 0) {
      return (this.maxHeap.top() + this.minHeap.top()) / 2;
    }
    return this.maxHeap.top();
  }
  return undefined;
};

/** 
 * Your MedianFinder object will be instantiated and called as such:
 * var obj = new MedianFinder()
 * obj.addNum(num)
 * var param_2 = obj.findMedian()
 */
```

