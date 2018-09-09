# LC890. Find and Replace Pattern

### LeetCode

## Question

You have a list of words and a pattern, and you want to know which words in words matches the pattern.

A word matches the pattern if there exists a permutation of letters p so that after replacing every letter x in the pattern with p(x), we get the desired word.

(Recall that a permutation of letters is a bijection from letters to letters: every letter maps to another letter, and no two letters map to the same letter.)

Return a list of the words in words that match the given pattern. 

You may return the answer in any order.

**Example 1:**
```
Input: words = ["abc","deq","mee","aqq","dkd","ccc"], pattern = "abb"
Output: ["mee","aqq"]
Explanation: "mee" matches the pattern because there is a permutation {a -> m, b -> e, ...}. 
"ccc" does not match the pattern because {a -> c, b -> c, ...} is not a permutation,
since a and b map to the same letter.
``` 

**Note:**

* 1 <= words.length <= 50
* 1 <= pattern.length = words[i].length <= 20

## Solutions

* Scala1
```
object Solution {
    def findAndReplacePattern(words: Array[String], pattern: String): List[String] = {
        words.filter(word => doesMatch(word, pattern)).toList
    }
    
    def doesMatch(word: String, pattern: String): Boolean = {
        val letterPair = word.zip(pattern).toSet
        val left = letterPair.map(letters => letters._1).toSet.size
        val right = letterPair.map(letters => letters._2).toSet.size
        letterPair.size==left && letterPair.size==right
    }
}
```

* Scala2
```
object Solution {
    def findAndReplacePattern(words: Array[String], pattern: String): List[String] = {
        words.filter(word => doesMatch(word, pattern)).toList
    }
    
    def doesMatch(word: String, pattern: String): Boolean = {
        val letterPair = word.zip(pattern).toSet.size
        val left = word.toSet.size
        val right = pattern.toSet.size
        letterPair==left && letterPair==right
    }
}
```

* Scala3
```
object Solution {
    def findAndReplacePattern(words: Array[String], pattern: String): List[String] = {
        val patternIndexes = getIndexes(pattern)
        words.filter(word => getIndexes(word).sameElements(patternIndexes)).toList
    }
    
    def getIndexes(word: String): List[Int] = {
        word.toList.map(w => word.indexOf(w))
    }
}
```

## Explanation

**Scala1 and Scala2**

Zip a word and the pattern, using set to remove duplicated pairs. Their sizes should be equal.

**Scala3**

Record the letter index in the String, the same letter should have the same index.

* **worst-case time complexity:** O(N * M), where `N` is the size of the input Array `words`, `M` is the length of the String `pattern`.
* **worst-case space complexity:** O(N * M), where `N` is the size of the input Array `words`, `M` is the length of the String `pattern`.

