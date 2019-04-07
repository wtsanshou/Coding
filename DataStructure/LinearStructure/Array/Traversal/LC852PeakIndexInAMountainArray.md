# LC852. Peak Index in a Mountain Array

### LeetCode

## Question

Let's call an array A a mountain if the following properties hold:

* A.length >= 3
* There exists some 0 < i < A.length - 1 such that A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1]

Given an array that is definitely a mountain, return any i such that A[0] < A[1] < ... A[i-1] < A[i] > A[i+1] > ... > A[A.length - 1].

**Example 1:**
```
Input: [0,1,0]
Output: 1
```

**Example 2:**
```
Input: [0,2,1,0]
Output: 1
```

**Note:**

* 3 <= A.length <= 10000
* 0 <= A[i] <= 10<sup>6</sup>
*A is a mountain, as defined above.

## Solutions

* Java1
```
public int peakIndexInMountainArray(int[] A) {
    int i=0;
    for(; i<A.length-1; ++i)
        if(A[i] > A[i+1]) break;
    return i;
}
```

* Scala
```
def peakIndexInMountainArray(A: Array[Int]): Int = {
    for(i <- 1 until A.length-1)
        if(((A(i)-A(i-1)).toLong * (A(i)-A(i+1)).toLong) > 0) return i
    1
}
```

## Explanation

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)
