
##   Word Ladder

A **transformation sequence** from word ```beginWord``` to word ```endWord``` using a dictionary ```wordList``` is a sequence of words ```beginWord -> s1 -> s2 -> ... -> sk``` such that:

- ``Every adjacent pair of words differs by a single letter.``
- ```Every si for 1 <= i <= k is in wordList. Note that beginWord does not need to be in wordList.```
- ```sk == endWord```

Given two words, ```beginWord``` and ```endWord```, and a dictionary ```wordList```, ***```return the number of words in the shortest transformation sequence from beginWord to endWord, or 0 if no such sequence exists.```***

**Example 1**
```bash
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.
```

**Example 2**
```bash
Input: beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
Output: 0
Explanation: The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.
```

### Constraints

- ```1 <= beginWord.length <= 10```
- ```endWord.length == beginWord.length```
- ```1 <= wordList.length <= 5000```
- ```wordList[i].length == beginWord.length```
- ```beginWord, endWord, and wordList[i] consist of lowercase English letters.```
- ```beginWord != endWord```
- ```All the words in wordList are unique.```

**Follow up:** Could you find an algorithm that runs in ```O(m + n)``` time?
 
## Solution
```javascript
const genNextWords = (word, wordSet) => {
    const nextWords = [];
    for(let i=0;i<word.length;i++) {
        for(let j=0;j<26;j++){
            const char = String.fromCharCode(97+j);
            if(char === word[i]) continue;

            const newWord= word.slice(0,i) + char + word.slice(i+1);
            if(wordSet.has(newWord)) {
                nextWords.push(newWord);
            }
        }
    }
    return nextWords;
}

/**
 * @param {string} beginWord
 * @param {string} endWord
 * @param {string[]} wordList
 * @return {number}
 */
var ladderLength = function(beginWord, endWord, wordList) {
    const wordSet = new Set(wordList);
    if(!wordSet.has(endWord)) return 0;

    const queue = [];
    queue.push(beginWord);
    const visited = new Set();
    visited.add(beginWord);
    let lvl = 1;

    while(queue.length > 0) {
        const size = queue.length;
        for(let i=0;i<size;i++) {
            const curWord = queue.shift();
            if(curWord === endWord) {
                return lvl;
            }

            const nextWords = genNextWords(curWord, wordSet);
            for(const word of nextWords) {
                if(!visited.has(word)) {
                    visited.add(word);
                    queue.push(word);
                }
            }
        }
        lvl++;
    }
    return 0;
};
```

