# LC893. Groups of Special-Equivalent Strings

### LeetCode

## Question

You are given an array A of strings.

Two strings S and T are special-equivalent if after any number of moves, S == T.

A move consists of choosing two indices i and j with i % 2 == j % 2, and swapping S[i] with S[j].

Now, a group of special-equivalent strings from A is a non-empty subset S of A such that any string not in S is not special-equivalent with any string in S.

Return the number of groups of special-equivalent strings from A.

**Example 1:**
```
Input: ["a","b","c","a","c","c"]
Output: 3
Explanation: 3 groups ["a","a"], ["b"], ["c","c","c"]
```

**Example 2:**
```
Input: ["aa","bb","ab","ba"]
Output: 4
Explanation: 4 groups ["aa"], ["bb"], ["ab"], ["ba"]
```

**Example 3:**
```
Input: ["abc","acb","bac","bca","cab","cba"]
Output: 3
Explanation: 3 groups ["abc","cba"], ["acb","bca"], ["bac","cab"]
```

**Example 4:**
```
Input: ["abcd","cdab","adcb","cbad"]
Output: 1
Explanation: 1 group ["abcd","cdab","adcb","cbad"]
```

**Note:**

* 1 <= A.length <= 1000
* 1 <= A[i].length <= 20
* All A[i] have the same length.
* All A[i] consist of only lowercase letters.

## Solutions

* Scala1
```
object Solution {
    def numSpecialEquivGroups(A: Array[String]): Int = {
        A.map(a => oddEvenSort(a)).toSet.size
    }
    
    def oddEvenSort(a: String): String = {
        val odd  = a.zipWithIndex.filter(_._2%2 == 1).map(_._1).sorted.mkString
        val even = a.zipWithIndex.filter(_._2%2 == 0).map(_._1).sorted.mkString
        odd ++ even
    }
}
```

## Explanation

Sort odd and even chars in the String. Convert the Array to unique set.

There is a faster algorithm Bucket Sort, but It's not easy to use Scala. Because Scala prefer immutable.

* **worst-case time complexity:** O(n * s*log(s)), where `n` is the size of the Array `A`, s is the maximum length in the string array.
* **worst-case space complexity:** O(n), where `n` is the size of the Array `A`.

