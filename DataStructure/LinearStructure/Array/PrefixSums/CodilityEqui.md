# Codility. Equi

### Codility

## Question

This is a demo task.

A zero-indexed array A consisting of N integers is given. An equilibrium index of this array is any integer P such that 0 ≤ P < N and the sum of elements of lower indices is equal to the sum of elements of higher indices, i.e. 

`A[0] + A[1] + ... + A[P−1] = A[P+1] + ... + A[N−2] + A[N−1].`

Sum of zero elements is assumed to be equal to 0. This can happen if P = 0 or if P = N−1.

For example, consider the following array A consisting of N = 8 elements:

```
A[0] = -1 
A[1] = 3 
A[2] = -4 
A[3] = 5 
A[4] = 1 
A[5] = -6 
A[6] = 2 
A[7] = 1
```

P = 1 is an equilibrium index of this array, because:

`A[0] = −1 = A[2] + A[3] + A[4] + A[5] + A[6] + A[7]`

P = 3 is an equilibrium index of this array, because:

`A[0] + A[1] + A[2] = −2 = A[4] + A[5] + A[6] + A[7]`

P = 7 is also an equilibrium index, because:

`A[0] + A[1] + A[2] + A[3] + A[4] + A[5] + A[6] = 0`

and there are no elements with indices greater than 7.

P = 8 is not an equilibrium index, because it does not fulfill the condition 0 ≤ P < N.

**Write a function:**

`int solution(vector<int> &A);`

that, given a zero-indexed array A consisting of N integers, returns any of its equilibrium indices. The function should return −1 if no equilibrium index exists.

For example, given array A shown above, the function may return 1, 3 or 7, as explained above.

**Assume that:**

* N is an integer within the range [0..100,000];
* each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
int solution(vector<int> &A) {
    // write your code in C++14 (g++ 6.2.0)
    int n = A.size();
    vector<long> left(n);
    vector<long> right(n);
    for(int i=1; i<n; ++i)
    {
        left[i] = left[i-1] + A[i-1];
        right[n-i-1] = right[n-i] + A[n-i];
    }
    for(int i=0; i<n; ++i)
        if(left[i] == right[i])
            return i;
    return -1;
}
```

## Explanation

The same as <a href="LC724FindPivotIndex.md">LC724. Find Pivot Index</a>

## Testcase

simple

extreme_large_numbers  Sequence with extremely large numbers testing arithmetic overflow.

extreme_negative_numbers  Sequence with extremely large numbers testing arithmetic overflow.

overflow_tests1  arithmetic overflow tests

overflow_tests2  arithmetic overflow tests

one_large  one large number at the end of the sequence

sum_0  sequence with sum=0

single_empty  single number or empty array

combinations_of_two  multiple runs, all pairs of values: -1, 0 and 1

combinations_of_three  multiple runs, all triples of values -1, 0 and 1

small_pyramid

extreme_max  Maximal size test

large_long_sequence_of_ones

large_long_sequence_of_minus_ones

medium_pyramid

large_pyramid  Large performance test, O(n^2) solutions should fail.

huge_pyramid  Large performance test, O(n^2) solutions should fail.


