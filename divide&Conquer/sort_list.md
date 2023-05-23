
##   Sort List

Given the ```head``` of a linked list, return ***```the list after sorting it in ascending order```***.

 


 


 


![sort_list_1](https://user-images.githubusercontent.com/118065908/235088495-7ab9880a-7b46-4c7c-9129-d53823f71e49.jpg)


**Example 1**
```bash
Input: head = [4,2,1,3]
Output: [1,2,3,4]
```
![sort_list_2](https://user-images.githubusercontent.com/118065908/235088500-89bb45c8-6109-4cea-bb6b-ae59036066bc.jpg)

**Example 2**
```bash
Input: head = [-1,5,3,4,0]
Output: [-1,0,3,4,5]
```

**Example 3**
```bash
Input: head = []
Output: []
```

### Constraints

- ```The number of nodes in the list is in the range [0, 5 * 104].```
- ```-105 <= Node.val <= 105```

***```Follow up:```*** Can you sort the linked list in O(n logn) time and O(1) memory (i.e. constant space)?

## Solution

```javascript
    /**
     * Definition for singly-linked list.
     * function ListNode(val, next) {
     *     this.val = (val===undefined ? 0 : val)
     *     this.next = (next===undefined ? null : next)
     * }
     */

    /**
     * @param {ListNode} head
     * @return {ListNode}
     */

 const merge = (l1, l2) => {
     if(!l1) return l2;
     if(!l2) return l1;

     const l = new ListNode(0);
     let cur = l;
     while(l1 && l2) {
         if(l1.val < l2.val) {
            cur.next = l1;
            l1 = l1.next;
         } else {
            cur.next = l2;
            l2 = l2.next;
         }
         cur=cur.next;
     }

     if(l1) cur.next = l1;
     if(l2) cur.next = l2;
     return l.next;
 }
 
var sortList = function(head) {
    if(!head || !head.next) return head;

    let q = head, p = head.next;
    while(p && p.next) {
        q=q.next;
        p=p.next.next;
    }

    const right = sortList(q.next);
    q.next = null;
    const left = sortList(head);
    return merge(left, right);
};
```
