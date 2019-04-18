# Codility. Max Slice Sum

### Codility

## Question

A non-empty zero-indexed array A consisting of N integers is given. A pair of integers (P, Q), such that 0 ≤ P ≤ Q < N, is called a slice of array A. The sum of a slice (P, Q) is the total of A[P] + A[P+1] + ... + A[Q].

**Write a function:**

`int solution(vector<int> &A);`

that, given an array A consisting of N integers, returns the maximum sum of any slice of A.

**For example, given array A such that:**

```
A[0] = 3 A[1] = 2 A[2] = -6 A[3] = 4 A[4] = 0

the function should return 5 because:

•	(3, 4) is a slice of A that has sum 4,
•	(2, 2) is a slice of A that has sum −6,
•	(0, 1) is a slice of A that has sum 5,
•	no other slice of A has sum greater than (0, 1).
```

**Assume that:**

* N is an integer within the range [1..1,000,000];
* each element of array A is an integer within the range [−1,000,000..1,000,000];
* the result will be an integer within the range [−2,147,483,648..2,147,483,647].

Complexity:
•	expected worst-case time complexity is O(N);
•	expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++
```
int solution(vector<int> &A) {
    int res = -1000000, sum = 0;
    for(int a : A)
    {
        sum = max(sum+a, a);
        res = max(res, sum);
    }
    return res;
}
```

* Java
```
public int solution(int[] A) {
    int maxSum = A[0];
    int cur = 0;
    for(int i=0; i<A.length; ++i){
        cur += A[i];
        maxSum = Math.max(maxSum, cur);
        if(cur<0) cur = 0;
    }
    return maxSum;
}
```

Using one pointer to memorying the maximum sum of left elements.

**Complexity:**

* **worst-case time complexity:** `O(N)`, where `N` is length of `A`.
* **worst-case space complexity:** `O(1)`.

## Testcase

one_element


two_elements


three_elements


simple


extreme_minimum


fifty_random


neg_const


pos_const


high_low_1Kgarbage


1Kgarbage_high_low


growing_saw


blocks


growing_negative

