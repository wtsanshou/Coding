# Codility. Count Distinct Slices

### Codility

## Question

An integer M and a non-empty zero-indexed array A consisting of N non-negative integers are given. All integers in array A are less than or equal to M.

A pair of integers (P, Q), such that 0 ≤ P ≤ Q < N, is called a slice of array A. The slice consists of the elements A[P], A[P + 1], ..., A[Q]. A distinct slice is a slice consisting of only unique numbers. That is, no individual number occurs more than once in the slice.

For example, consider integer M = 6 and array A such that:

```
A[0] = 3 A[1] = 4 A[2] = 5 A[3] = 5 A[4] = 2

There are exactly nine distinct slices: 

(0, 0), (0, 1), (0, 2), (1, 1), (1, 2), (2, 2), (3, 3), (3, 4) and (4, 4).

The goal is to calculate the number of distinct slices.
```

**Write a function:**

`int solution(int M, vector<int> &A);`

that, given an integer M and a non-empty zero-indexed array A consisting of N integers, returns the number of distinct slices.

If the number of distinct slices is greater than 1,000,000,000, the function should return 1,000,000,000.

For example, given integer M = 6 and array A such that:

`A[0] = 3 A[1] = 4 A[2] = 5 A[3] = 5 A[4] = 2`

the function should return 9, as explained above.

**Assume that:**

* N is an integer within the range [1..100,000];
* M is an integer within the range [0..100,000];
* each element of array A is an integer within the range [0..M].

Complexity:
•	expected worst-case time complexity is O(N);
•	expected worst-case space complexity is O(M), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

### Solution 1

* C++
```
int solution(int M, vector<int> &A) {
    vector<int> map(M+1, -1);
    long res = 0; 
    int start = 0, n = A.size();
    for(unsigned int i=0; i<A.size(); ++i)
    {
        if(map[A[i]] >= start)
        {
            res += (long)(i-start)*(i-start+1)/2;
            start = map[A[i]]+1;
            res -= (long)(i-start)*(i-start+1)/2;
            if(res > 1e9) return 1e9;
        }
        map[A[i]] = i;
    }
    res += (long)(n-start)*(n-start+1)/2;
    return (res > 1e9) ?  1e9 : res;
}
```

Using a map to memory the location of numbers in `A`. When found a duplicated number (`map[A[i]] >= start`):

1. Plus the number of combination from (start ~ i).
2. Minus the number of combination from (previous duplicated number's location + 1  ~ i). This number is the number of combination with duplicate elements.

**Note:** Don't forget to add the final number of combination.

## Testcase

single 

single element


double 

double elements


simple1 

first simple test


simple2 

second simple test


small_random 

small random test, length = 100


medium_random 

medium random test, length = 500


large 

large tests, length = ~100,000


large_range 

large range tests, length = ~100,000


large_random 

large random tests, length = ~100,000


extreme_the_same 

all the same elements, length = ~100,000

