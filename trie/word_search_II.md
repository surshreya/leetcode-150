
## Word Search II

Given an ```m x n``` ***board of characters*** and a ***list of strings words***, ```return all words on the board.```

Each word must be constructed from letters of sequentially **adjacent cells**, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

 


 ![search1](https://github.com/surshreya/leetcode-150/assets/118065908/9d05400a-d8fe-44b8-987b-bc5de32322d1)


**Example 1**
```bash
Input: board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]], words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```

![search2](https://github.com/surshreya/leetcode-150/assets/118065908/6e0069b3-3393-4501-a138-93b6df6121a7)

**Example 2**
```bash
Input: board = [["a","b"],["c","d"]], words = ["abcb"]
Output: []
```

### Constraints
- m == board.length
- n == board[i].length
- 1 <= m, n <= 12
- board[i][j] is a lowercase English letter.
- 1 <= words.length <= 3 * 104
- 1 <= words[i].length <= 10
- words[i] consists of lowercase English letters.
- All the strings of words are unique.

## Solution

```javascript
class TrieNode {
  constructor() {
    this.children = new Map();
    this.word = null;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let node = this.root;
    for (let char of word) {
      if (!node.children.has(char)) {
        node.children.set(char, new TrieNode());
      }
      node = node.children.get(char);
    }
    node.word = word;
  }
}

/**
 * @param {character[][]} board
 * @param {string[]} words
 * @return {string[]}
 */
var findWords = function(board, words) {
    const result = [];
    const trie = new Trie();

    for(const word of words) {
        trie.insert(word);
    }

    const dfs = function (node, r, c) {
      const validRow = r >= 0 && r < board.length;
      const validCol = c >= 0 && c < board[0].length;

      if (!validRow || !validCol) return false;
      const char = board[r][c];
      if (char === '#' || !node.children.has(char)) {
        return;
      }

      node = node.children.get(char);
      if (node.word) {
        result.push(node.word);
        node.word = null; 
      }

      board[r][c] = '#'; 

      dfs(node, r-1, c);
      dfs(node, r+1, c);
      dfs(node, r, c-1);
      dfs(node, r, c+1);

      board[r][c] = char;
    }

    for (let row = 0; row < board.length; row++) {
        for (let col = 0; col < board[0].length; col++) {
            dfs(trie.root, row, col);
        }
    }

  return result;
};
```
