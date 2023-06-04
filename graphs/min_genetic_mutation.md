
##  Minimum Genetic Mutation

A gene string can be represented by an ```8-character``` long string, with choices from ```'A', 'C', 'G', and 'T'.```

Suppose we need to investigate a mutation from a gene string ```startGene``` to a gene string ```endGene``` where one mutation is defined as one single character changed in the gene string.

- For example, ```"AACCGGTT" --> "AACCGGTA"``` is one mutation.
There is also a gene ```bank``` bank that records all the valid gene mutations.``` A gene must be in bank to make it a valid gene string.```

Given the two gene strings ```startGene``` and ```endGene``` and the gene bank bank, ```return the minimum number of mutations needed to mutate from startGene to endGene```. If there is no such a mutation, return ```-1```.

**Note** that the starting point is assumed to be valid, so it might not be included in the bank.

 

 

 

**Example 1**
```bash
Input: startGene = "AACCGGTT", endGene = "AACCGGTA", bank = ["AACCGGTA"]
Output: 1
```

**Example 2**
```bash
Input: startGene = "AACCGGTT", endGene = "AAACGGTA", bank = ["AACCGGTA","AACCGCTA","AAACGGTA"]
Output: 2
```

### Constraints

- ```0 <= bank.length <= 10```
- ```startGene.length == endGene.length == bank[i].length == 8```
- ```startGene, endGene, and bank[i] consist of only the characters ['A', 'C', 'G', 'T'].```
 
## Solution

```javascript
/**
 * @param {string} startGene
 * @param {string} endGene
 * @param {string[]} bank
 * @return {number}
 */
var minMutation = function(startGene, endGene, bank) {
    const queue = [[startGene, 0]];
    const bankset = new Set(bank);
    const mutations = ['A', 'C', 'G', 'T'];

    while(queue.length > 0) {
        const [currentGene, level] = queue.shift();
        
        if(currentGene === endGene) {
            return level;
        }

        for(let i=0 ; i<currentGene.length; i++) {
            for(let j=0; j<mutations.length; j++) {
                if(currentGene[i] === mutations[j]) continue;

                const mutatedGene = currentGene.slice(0, i) + mutations[j] + currentGene.slice(i + 1);
                if(bankset.has(mutatedGene)) {
                    queue.push([mutatedGene, level+1]);
                    bankset.delete(mutatedGene);
                }
            }
        }
    }

    return -1;
};
```

