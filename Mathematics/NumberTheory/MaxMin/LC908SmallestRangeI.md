# LC908. Smallest Range I

### LeetCode

## Question

Given an array A of integers, for each integer A[i] we may choose any x with -K <= x <= K, and add x to A[i].

After this process, we have some array B.

Return the smallest possible difference between the maximum value of B and the minimum value of B.

**Example 1:**
```
Input: A = [1], K = 0
Output: 0
Explanation: B = [1]
```

**Example 2:**
```
Input: A = [0,10], K = 2
Output: 6
Explanation: B = [2,8]
```

**Example 3:**
```
Input: A = [1,3,6], K = 3
Output: 0
Explanation: B = [3,3,3] or B = [4,4,4]
```

## Solutions

* Scala1
```
def smallestRangeI(A: Array[Int], K: Int): Int = {
    Math.max(A.max - A.min - 2*K, 0)
}
```

## Explanation

The max and min values of `B` are from the max and min values of `A`.

1. If the range (`A.max - A.min`) is larger than `2*K`, the range can be reduced by `2*K`.
2. else, the smallest possible difference is `0`.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the array `A`.
* **worst-case space complexity:** `O(1)`.
