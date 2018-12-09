# LC944. Delete Columns to Make Sorted

### LeetCode

## Question

We are given an array A of N lowercase letter strings, all of the same length.

Now, we may choose any set of deletion indices, and for each string, we delete all the characters in those indices.

For example, if we have an array A = ["abcdef","uvwxyz"] and deletion indices {0, 2, 3}, then the final array after deletions is ["bef", "vyz"], and the remaining columns of A are ["b","v"], ["e","y"], and ["f","z"].  (Formally, the c-th column is [A[0][c], A[1][c], ..., A[A.length-1][c]].)

Suppose we chose a set of deletion indices D such that after deletions, each remaining column in A is in non-decreasing sorted order.

Return the minimum possible value of D.length.

**Example 1:**
```
Input: ["cba","daf","ghi"]
Output: 1
Explanation: 
After choosing D = {1}, each column ["c","d","g"] and ["a","f","i"] are in non-decreasing sorted order.
If we chose D = {}, then a column ["b","a","h"] would not be in non-decreasing sorted order.
```

**Example 2:**
```
Input: ["a","b"]
Output: 0
Explanation: D = {}
```

**Example 3:**
```
Input: ["zyx","wvu","tsr"]
Output: 3
Explanation: D = {0, 1, 2}
```

**Note:**

* 1 <= A.length <= 100
* 1 <= A[i].length <= 1000

## Solutions

* Scala1
```
object Solution {
    def minDeletionSize(A: Array[String]): Int = {
        val transpose = A.map(a => a.toCharArray()).transpose
        transpose.filter(isNotSorted(_)).length
    }
    
    def isNotSorted(arr: Array[Char]): Boolean = {
        for( i <- 0 until arr.length-1){
            if(arr(i) > arr(i+1)) return true
        }
        false
    }
}
```

## Explanation

Scala is not good at solving columns, so using transpose to change the columns to rows. Then filter the unsorted rows in.

* **worst-case time complexity:** O(m * n), where `m` is the lenght of the Array, n is the lenght of the String in the array.
* **worst-case space complexity:** O(m * n), where `m` is the lenght of the Array, n is the lenght of the String in the array.


