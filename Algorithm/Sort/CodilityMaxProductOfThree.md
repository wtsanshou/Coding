# Codility. Max Product Of Three

### Codility

## Question

Maximize A[P] * A[Q] * A[R] for any triplet (P, Q, R).

A non-empty array A consisting of N integers is given. The product of triplet (P, Q, R) equates to A[P] * A[Q] * A[R] (0 ≤ P < Q < R < N).

For example, array A such that:

`A[0] = -3 A[1] = 1 A[2] = 2 A[3] = -2 A[4] = 5 A[5] = 6`

contains the following example triplets:

* (0, 1, 2), product is −3 * 1 * 2 = −6
* (1, 2, 4), product is 1 * 2 * 5 = 10
* (2, 4, 5), product is 2 * 5 * 6 = 60

Your goal is to find the maximal product of any triplet.

**Write a function:**

`class Solution { public int solution(int[] A); }`

that, given a non-empty array A, returns the value of the maximal product of any triplet.

For example, given array A such that:

`A[0] = -3 A[1] = 1 A[2] = 2 A[3] = -2 A[4] = 5 A[5] = 6`

the function should return 60, as the product of triplet (2, 4, 5) is maximal.
Write an efficient algorithm for the following assumptions:

* N is an integer within the range [3..100,000];
* each element of array A is an integer within the range [−1,000..1,000].

## Solutions

### Solution 1

* Java
```
public int solution(int[] A) {
    Arrays.sort(A);
    int n = A.length;
    return Math.max(A[0]*A[1]*A[n-1], A[n-3]*A[n-2]*A[n-1]);
}
```

Only two situations product the maximal triplet:

1. The maximum 3 numbers in the `A`
2. The maximum 1 number and 2 minimum numbers (2 negative numbers)

**Complexity:**

* **worst-case time complexity:** `O(N * log(N))`, where `N` is the size of the input `A`.
* **worst-case space complexity:** `O(log(N))`, where `N` is the size of the input `A`.
