
##   Construct Quad Tree

Given a ```n * n``` matrix grid of ```0's``` and ```1's``` only. We want to represent grid with a Quad-Tree.

```Return the root of the Quad-Tree representing grid.```

A **Quad-Tree** is a tree data structure in which each internal node has ***exactly four children.*** Besides, each node has **two** attributes:

- ```val:``` True if the node represents a grid of 1's or False if the node represents a grid of 0's. Notice that you can assign the val to True or False when isLeaf is False, and both are accepted in the answer.
- ```isLeaf:``` True if the node is a leaf node on the tree or False if the node has four children.
 
 ```
 class Node {
    public boolean val;
    public boolean isLeaf;
    public Node topLeft;
    public Node topRight;
    public Node bottomLeft;
    public Node bottomRight;
}
```

We can construct a Quad-Tree from a two-dimensional area using the following steps:

If the current grid has the same value (i.e all ```1's``` or all ```0's```) set isLeaf True and set val to the value of the grid and set the four children to Null and stop.
If the current grid has different values, set ```isLeaf``` to ```False``` and set ```val``` to any value and ***divide the current grid into four sub-grids as shown in the photo.***
Recurse for each of the children with the proper sub-grid.

<img width="831" alt="new_top" src="https://github.com/surshreya/leetcode-150/assets/118065908/a736084b-24d4-4d29-8070-3db5c23e123b">


If you want to know more about the Quad-Tree, you can refer to the wiki.

**Quad-Tree format:**

You don't need to read this section for solving the problem. This is only if you want to understand the output format here. The output represents the serialized format of a Quad-Tree using level order traversal, where null signifies a path terminator where no node exists below.

It is very similar to the serialization of the binary tree. The only difference is that the node is represented as a list ```[isLeaf, val]```.

If the value of isLeaf or val is True we represent it as ```1``` in the list ```[isLeaf, val]``` and if the value of ```isLeaf or val``` is False we represent it as ```0```.



**Example 1**

![grid1](https://github.com/surshreya/leetcode-150/assets/118065908/3bfdc3fd-2243-4745-b221-b8abfa16ef49)

```bash
Input: grid = [[0,1],[1,0]]
Output: [[0,1],[1,0],[1,1],[1,1],[1,0]]
Explanation: The explanation of this example is shown below:
Notice that 0 represnts False and 1 represents True in the photo representing the Quad-Tree.
```
![e1tree](https://github.com/surshreya/leetcode-150/assets/118065908/73c96571-ac5d-47d1-9286-9b306fb478d2)



**Example 2**

![e2mat](https://github.com/surshreya/leetcode-150/assets/118065908/d3ef5786-c6c1-41f6-a9cd-aa197b3aacd1)

```bash
Input: grid = [[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,1,1,1,1],[1,1,1,1,1,1,1,1],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0],[1,1,1,1,0,0,0,0]]
Output: [[0,1],[1,1],[0,1],[1,1],[1,0],null,null,null,null,[1,0],[1,0],[1,1],[1,1]]
Explanation: All values in the grid are not the same. We divide the grid into four sub-grids.
The topLeft, bottomLeft and bottomRight each has the same value.
The topRight have different values so we divide it into 4 sub-grids where each has the same value.
Explanation is shown in the photo below:
```

![e2tree](https://github.com/surshreya/leetcode-150/assets/118065908/5e9c28f4-d45b-4d5f-b785-0ef154774ecf)



### Constraints
- n == grid.length == grid[i].length
- n == 2x where 0 <= x <= 6


## Solution

```javascript
/**
 * // Definition for a QuadTree node.
 * function Node(val,isLeaf,topLeft,topRight,bottomLeft,bottomRight) {
 *    this.val = val;
 *    this.isLeaf = isLeaf;
 *    this.topLeft = topLeft;
 *    this.topRight = topRight;
 *    this.bottomLeft = bottomLeft;
 *    this.bottomRight = bottomRight;
 * };
 */

 const isSame = (row, col, size, grid) => {
     const value = grid[row][col];

     for(let i=row;i<row+size;i++) {
         for(let j=col;j<col+size;j++) {
             if(grid[i][j] !== value) {
                 return false;
             }
         }
     }

     return true;
 }

const buildTree = (row, col, size, grid) => {
    if(isSame(row,col,size,grid)) {
        return new Node(grid[row][col] === 1, true, null, null, null, null);
    } else {
        const n = size/2;
        const topLeft = buildTree(row,col,n,grid);
        const topRight = buildTree(row,col+n,n,grid);
        const bottomLeft = buildTree(row+n,col,n,grid);
        const bottomRight = buildTree(row+n,col+n,n,grid);
        return new Node(false, false, topLeft, topRight, bottomLeft, bottomRight);
    }
}

/**
 * @param {number[][]} grid
 * @return {Node}
 */
var construct = function(grid) {
    const n = grid.length;
    return buildTree(0,0,n,grid);
};
```
