## Find K Pairs with Smallest Sums

You are given two integer arrays `nums1` and `nums2` sorted in **ascending** order and an integer `k`.

Define a pair `(u, v)` which consists of one element from the first array and one element from the second array.

`Return the k pairs (u1, v1), (u2, v2), ..., (uk, vk) with the smallest sums.`

**Example 1**

```bash
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]]
Explanation: The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

**Example 2**

```bash
Input: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
Output: [[1,1],[1,1]]
Explanation: The first 2 pairs are returned from the sequence: [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

**Example 3**

```bash
Input: nums1 = [1,2], nums2 = [3], k = 3
Output: [[1,3],[2,3]]
Explanation: All possible pairs are returned from the sequence: [1,3],[2,3]
```

### Constraints

- `1 <= nums1.length, nums2.length <= 105`
- `-109 <= nums1[i], nums2[i] <= 109`
- `nums1 and nums2 both are sorted in ascending order.`
- `1 <= k <= 104`

## Solution

```javascript
class HeapNode {
  constructor(i, j, val) {
    this.i = i;
    this.j = j;
    this.val = val;
  }
}

class MinHeap {
  constructor() {
    this.heap = [];
  }
  size() {
    return this.heap.length;
  }
  isEmpty() {
    return this.heap.length === 0;
  }
  push(node) {
    this.heap.push(node);
    this.heapifyUp(this.heap.length - 1);
  }
  pop() {
    if (this.isEmpty()) return null;
    const min = this.heap[0];
    const last = this.heap.pop();
    if (!this.isEmpty()) {
      this.heap[0] = last;
      this.heapifyDown(0);
    }

    return min;
  }
  swap(i, j) {
    const temp = this.heap[i];
    this.heap[i] = this.heap[j];
    this.heap[j] = temp;
  }
  heapifyUp(index) {
    let currIndex = index;

    while (currIndex > 0) {
      const parentIndex = Math.floor((currIndex - 1) / 2);
      if (this.heap[parentIndex].val <= this.heap[currIndex].val) {
        break;
      }
      this.swap(currIndex, parentIndex);
      currIndex = parentIndex;
    }
  }
  heapifyDown(index) {
    let currIndex = index;
    const lastIndex = this.heap.length - 1;

    while (true) {
      let smallestIndex = currIndex;
      const leftChild = 2 * currIndex + 1;
      const rightChild = 2 * currIndex + 2;

      if (
        leftChild <= lastIndex &&
        this.heap[leftChild].val < this.heap[smallestIndex].val
      ) {
        smallestIndex = leftChild;
      }

      if (
        rightChild <= lastIndex &&
        this.heap[rightChild].val < this.heap[smallestIndex].val
      ) {
        smallestIndex = rightChild;
      }

      if (smallestIndex !== currIndex) {
        this.swap(currIndex, smallestIndex);
        currIndex = smallestIndex;
      } else {
        break;
      }
    }
  }
}
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number[][]}
 */
var kSmallestPairs = function (nums1, nums2, k) {
  if (!nums1.length || !nums2.length || !k) {
    return [];
  }

  const minHeap = new MinHeap();
  for (let i = 0; i < Math.min(nums1.length, k); i++) {
    minHeap.push(new HeapNode(i, 0, nums1[i] + nums2[0]));
  }

  const result = [];
  while (minHeap.size() > 0 && result.length < k) {
    const { i, j, val } = minHeap.pop();
    result.push([nums1[i], nums2[j]]);

    if (j + 1 < nums2.length) {
      minHeap.push(new HeapNode(i, j + 1, nums1[i] + nums2[j + 1]));
    }
  }

  return result;
};
```
