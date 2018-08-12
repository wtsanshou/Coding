# LC888. Uncommon Words from Two Sentences

### LeetCode

## Question

We are given two sentences A and B.  (A sentence is a string of space separated words.  Each word consists only of lowercase letters.)

A word is uncommon if it appears exactly once in one of the sentences, and does not appear in the other sentence.

Return a list of all uncommon words. 

You may return the list in any order.

**Example 1:**
```
Input: A = "this apple is sweet", B = "this apple is sour"
Output: ["sweet","sour"]
```

**Example 2:**
```
Input: A = "apple apple", B = "banana"
Output: ["banana"]
```

**Note:**

* 0 <= A.length <= 200
* 0 <= B.length <= 200
* A and B both contain only spaces and lowercase letters.

## Solutions

* Scala1
```
def uncommonFromSentences(A: String, B: String): Array[String] = {
    val abList = A.split(" ") ++: B.split(" ")
    abList.filter(x => x!="" && abList.count(x == _) == 1)
}
```

## Explanation

* **worst-case time complexity:** O((n+m)<sup>2</sup>), where 'n' is the number of words in String 'A', 'm' is the number of words in String 'B'. 
* **worst-case space complexity:** O((n+m)<sup>2</sup>), where 'n' is the number of words in String 'A', 'm' is the number of words in String 'B'. 