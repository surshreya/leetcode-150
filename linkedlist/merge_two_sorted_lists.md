
##   Merge Two Sorted Lists

You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists in a one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.




**Example 1**
```bash
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```
**Example 2**
```bash
Input: list1 = [], list2 = []
Output: []
```
**Example 3**
```bash
Input: list1 = [], list2 = [0]
Output: [0]
```
    
### Constraints

- ```The number of nodes in both lists is in the range [0, 50].```

- ```-100 <= Node.val <= 100```

- ``` Both list1 and list2 are sorted in non-decreasing order.```

## Solution

```javascript
class Node {
     constructor(val) {
         this.val = val;
         this.next = null;
     }
 }
var mergeTwoLists = function(list1, list2) {
    if(!list1) return list2;
    if(!list2) return list1;

    let merged = new Node(null);
    let cur = merged;

    while(list1 && list2) {
        if(list1.val < list2.val) {
            cur.next = list1;
            list1 = list1.next;
        } else {
            cur.next = list2;
            list2 = list2.next;
        }
        cur = cur.next;
    }

    if(list1) cur.next = list1;
    if(list2) cur.next = list2;
    return merged.next;
    
};
```
