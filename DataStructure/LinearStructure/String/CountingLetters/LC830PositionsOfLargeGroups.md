# LC830. Positions of Large Groups

### LeetCode

## Question

In a string S of lowercase letters, these letters form consecutive groups of the same character.

For example, a string like S = "abbxxxxzyy" has the groups "a", "bb", "xxxx", "z" and "yy".

Call a group large if it has 3 or more characters.  We would like the starting and ending positions of every large group.

The final answer should be in lexicographic order.

**Example 1:**
```
Input: "abbxxxxzzy"
Output: [[3,6]]
Explanation: "xxxx" is the single large group with starting  3 and ending positions 6.
```

**Example 2:**
```
Input: "abc"
Output: []
Explanation: We have "a","b" and "c" but no large group.
```

**Example 3:**
```
Input: "abcdddeeeeaabbbcd"
Output: [[3,5],[6,9],[12,14]]
```

**Note:**  1 <= S.length <= 1000

## Solutions

* Scala1
```
def largeGroupPositions(S: String): List[List[Int]] = {
    var res: List[List[Int]] = List()
    var start = 0
    val s = S.toArray
    for(i <- 1 to s.length-1; if(s.charAt(i) != s.charAt(i-1))){
        if(i - start >=3) res = res :+ List(start, i-1)
        start = i
    }
    if(s.length - start >= 3) res = res :+ List(start, s.length-1)
    res
}
```

## Explanation

Traversal the string, find all groups that larger than 3. 

Note don't miss the possible final one.

* **worst-case time complexity:** O(n), where n is the number of characters in the String.
* **worst-case space complexity:** O(n), where n is the number of characters in the String.

