
##   Text Justification


Given an array of strings ```words``` and a width ```maxWidth```, format the text such that ***```each line has exactly maxWidth characters and is fully (left and right) justified.```***

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ```' '``` when necessary so that each line has exactly ```maxWidth``` characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line does not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left-justified, and no extra space is inserted between words.

**Note:**

- A word is defined as a character sequence consisting of non-space characters only.
- Each word's length is guaranteed to be greater than 0 and not exceed maxWidth.
- The input array words contains at least one word.

 
 

**Example 1**
```bash
Input: words = ["This", "is", "an", "example", "of", "text", "justification."], maxWidth = 16
Output:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

**Example 2**
```bash
Input: words = ["What","must","be","acknowledgment","shall","be"], maxWidth = 16
Output:
[
  "What   must   be",
  "acknowledgment  ",
  "shall be        "
]
Explanation: Note that the last line is "shall be    " instead of "shall     be", because the last line must be left-justified instead of fully-justified.
Note that the second line is also left-justified because it contains only one word.
```

**Example 3**
```bash
Input: words = ["Science","is","what","we","understand","well","enough","to","explain","to","a","computer.","Art","is","everything","else","we","do"], maxWidth = 20
Output:
[
  "Science  is  what we",
  "understand      well",
  "enough to explain to",
  "a  computer.  Art is",
  "everything  else  we",
  "do                  "
]
```

### Constraints

- ```1 <= words.length <= 300```
- ```1 <= words[i].length <= 20```
- ```words[i] consists of only English letters and symbols.```
- ```1 <= maxWidth <= 100```
- ```words[i].length <= maxWidth```
 
## Solution
***```Solution 1- Greedy```***
```javascript
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
var fullJustify = function(words, maxWidth) {
    const result = [];
    let currLine = [];
    let currWidth = 0;

    for(let i=0;i<words.length;i++) {
        if(currWidth + currLine.length + words[i].length > maxWidth) {
            let line = '';
            let totalSpace = maxWidth - currWidth;

            if(currLine.length === 1) {
                line = currLine[0] + ' '.repeat(totalSpace);
            } else {
                const spacesBetween = Math.floor(totalSpace / (currLine.length - 1));
                const extraSpaces = totalSpace % (currLine.length - 1);
                for (let j = 0; j < currLine.length - 1; j++) {
                    line += currLine[j] + ' '.repeat(spacesBetween);
                    if (j < extraSpaces) {
                        line += ' ';
                    }
                }
                line += currLine[currLine.length - 1]; 
            }
            result.push(line);
            currLine = [];
            currWidth = 0;
        }
        currLine.push(words[i]);
        currWidth += words[i].length;
    }
    result.push(currLine.join(' ') + ' '.repeat(maxWidth - currWidth - currLine.length + 1));
    return result;
};
```

