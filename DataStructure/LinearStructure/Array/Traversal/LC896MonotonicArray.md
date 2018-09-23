# LC896. Monotonic Array

### LeetCode

## Question

An array is monotonic if it is either monotone increasing or monotone decreasing.

An array A is monotone increasing if for all i <= j, A[i] <= A[j].  An array A is monotone decreasing if for all i <= j, A[i] >= A[j].

Return true if and only if the given array A is monotonic.

**Example 1:**
```
Input: [1,2,2,3]
Output: true
```

**Example 2:**
```
Input: [6,5,4,4]
Output: true
```

**Example 3:**
```
Input: [1,3,2]
Output: false
```

**Example 4:**
```
Input: [1,2,4,5]
Output: true
```

**Example 5:**
```
Input: [1,1,1]
Output: true
``` 

**Note:**

* 1 <= A.length <= 50000
* -100000 <= A[i] <= 100000

## Solutions

* Scala1
```
def isMonotonic(A: Array[Int]): Boolean = {
    if(A.size <= 2) return true
    var result = A(1) - A(0)
    for(i <- 2 until A.size) {
        val cur = A(i)-A(i-1)
        if(result * cur < 0) return false
        if(cur != 0) result = cur
    }
    true
}
```

## Explanation

Keep previous sign, if found a opposite sign, return false.

* **worst-case time complexity:** O(n), where `n` is the size of the input array.
* **worst-case space complexity:** O(1)
