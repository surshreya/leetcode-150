
##   Copy List with Random Pointer

A linked list of length ***```n```*** is given such that each node contains an additional random pointer, which could point to any node in the list, or  ***```null```***.

Construct a  ***```deep copy```*** of the list. The deep copy should consist of exactly  ***```n brand new nodes```***, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. **None of the pointers in the new list should point to nodes in the original list.**

For example, if there are two nodes  ***```X```*** and  ***```Y```*** in the original list, where  ***```X.random --> Y```***, then for the corresponding two nodes  ***```x and y```*** in the copied list, ***```x.random --> y```***.

***```Return the head of the copied linked list.```***

The linked list is represented in the input/output as a list of n nodes. Each node is represented as a pair of ***```[val, random_index]```*** where:

- ```val```: an integer representing Node.val
- ```random_index```: the index of the node (range from 0 to n-1) that the random pointer points to, or null if it does not point to any node.
Your code will **only** be given the head of the original linked list.

 


 


 


![e1](https://user-images.githubusercontent.com/118065908/234943931-84300ccb-c015-4fc4-8986-91881a315e4d.png)


**Example 1**
```bash
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```
![e2](https://user-images.githubusercontent.com/118065908/234943951-a3b8e28e-3166-40a3-a0f0-a1981c17a8ec.png)

**Example 2**
```bash
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]]
```
![e3](https://user-images.githubusercontent.com/118065908/234943969-5135941e-601d-4564-a588-a586dd1415aa.png)

**Example 3**
```bash
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
```

### Constraints

- ```0 <= n <= 1000```
- ```-104 <= Node.val <= 104```
- ```Node.random is null or is pointing to some node in the linked list.```


## Solution

***```  Method 1 ```***
```javascript
/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
var copyRandomList = function(head) {
    const mp = new Map();
    let temp = head;

    while(temp) {
        const node = new Node(temp.val);
        mp.set(temp, node);
        temp=temp.next;
    }

    let temp1 = head;
    while(temp1) {
        let node = mp.get(temp1);
        node.next = temp1.next ? mp.get(temp1.next) : null;
        node.random = temp1.random ? mp.get(temp1.random) : null;
        temp1=temp1.next;
    }
    return mp.get(head);
};
```
