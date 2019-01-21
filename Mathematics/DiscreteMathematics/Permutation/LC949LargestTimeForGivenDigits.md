# LC949. Largest Time for Given Digits

### LeetCode

## Question

Given an array of 4 digits, return the largest 24 hour time that can be made.

The smallest 24 hour time is 00:00, and the largest is 23:59.  Starting from 00:00, a time is larger if more time has elapsed since midnight.

Return the answer as a string of length 5.  If no valid time can be made, return an empty string.

**Example 1:**
```
Input: [1,2,3,4]
Output: "23:41"
```

**Example 2:**
```
Input: [5,5,5,5]
Output: ""
```

**Note:**

* A.length == 4
* 0 <= A[i] <= 9

## Solutions

* Scala1
```
def largestTimeFromDigits(A: Array[Int]): String = {
    val permutations = A.permutations
    val times = permutations.filter(p => p(0)*10+p(1)<24 && p(2)*10+p(3)<60)
    if(times.isEmpty) return ""
    val t = times.foldLeft(Array(0,0,0,0)){ (z, t) =>
          if(t(0)*10+t(1) > z(0)*10+z(1) || (t(0)*10+t(1) == z(0)*10+z(1) && t(2)*10+t(3) > z(2)*10+z(3))) t
        else z
        }
    t(0).toString+t(1).toString + ":" + t(2).toString+t(3).toString
}
```

## Explanation

The number permutation of 4 digits is 24 `4!`. 

1. filter out all illegal times.
2. find the largest time.

* **worst-case time complexity:** `O(1)`. 
* **worst-case space complexity:** `O(1)`

