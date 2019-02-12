# LC941. Valid Mountain Array

### LeetCode

## Question

Given an array A of integers, return true if and only if it is a valid mountain array.

Recall that A is a mountain array if and only if:

A.length >= 3

There exists some i with 0 < i < A.length - 1 such that:

* A[0] < A[1] < ... A[i-1] < A[i]
* A[i] > A[i+1] > ... > A[B.length - 1]

**Example 1:**
```
Input: [2,1]
Output: false
```

**Example 2:**
```
Input: [3,5,5]
Output: false
```

**Example 3:**
```
Input: [0,3,2,1]
Output: true
``` 

**Note:**

* 0 <= A.length <= 10000
* 0 <= A[i] <= 10000 

## Solutions

* Java1
```
public boolean validMountainArray(int[] A) {
    if(A.length < 3) return false;
    return leftTop(A)==rightTop(A);
}

private int leftTop(int[] A){
    for(int l=1; l<A.length; ++l)
        if(A[l] <= A[l-1]) return l-1;
    return A.length;
}

private int rightTop(int[] A){
    for(int r=A.length-2; r>=0; --r)
        if(A[r] <= A[r+1]) return r+1;
    return -1;
}
```

## Explanation

a valid mountain array: the index of the left top should be equal to the index of the right top

* **worst-case time complexity:** `O(N)`, where `N` is the length of the array `A`.
* **worst-case space complexity:** O(1).