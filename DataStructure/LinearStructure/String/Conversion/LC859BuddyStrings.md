# LC859. Buddy Strings

### LeetCode

## Question

Given two strings A and B of lowercase letters, return true if and only if we can swap two letters in A so that the result equals B.

**Example 1:**
```
Input: A = "ab", B = "ba"
Output: true
```
**Example 2:**
```
Input: A = "ab", B = "ab"
Output: false
```

**Example 3:**
```
Input: A = "aa", B = "aa"
Output: true
```

**Example 4:**
```
Input: A = "aaaaaaabc", B = "aaaaaaacb"
Output: true
```

**Example 5:**
```
Input: A = "", B = "aa"
Output: false
``` 

**Note:**

* 0 <= A.length <= 20000
* 0 <= B.length <= 20000
* A and B consist only of lowercase letters.

## Solutions

* Scala1
```
def buddyStrings(A: String, B: String): Boolean = {
    var aList = List[Char]()
    var bList = List[Char]()
    A.zipWithIndex.foreach(a => {
        if(a._1 != B.charAt(a._2)) {
            aList = aList :+ a._1
            bList = bList :+ B.charAt(a._2)
        }
    })
    
    ((aList.isEmpty && A != A.distinct) || aList.size == 2) && aList == bList.reverse
}
```

* Scala2
```
def buddyStrings(A: String, B: String): Boolean = {
    val abDiff = A.zip(B).filter(ab => ab._1 != ab._2).map(ab => ab._1.toString + ab._2).mkString("")
    (abDiff.isEmpty && A != A.distinct) || (abDiff.size == 4 && abDiff == abDiff.reverse)
}
```

## Explanation

Find all different char pairs.

Two cases fullfill the `Buddy Strings:

1. No different between the two String `A` and `B`, but they must contain duplicate letter.
2. There is exactly 2 pairs of different chars, their string should equal to their reverse string.

* **worst-case time complexity:** **O(N)**, where `N` is the length of the Strings.
* **worst-case space complexity:** **O(N)**, where `N` is the length of the Strings.
