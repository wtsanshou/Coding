# Codility. Perm Check

### Codility

## Question

A non-empty zero-indexed array A consisting of N integers is given.

A permutation is a sequence containing each element from 1 to N once, and only once.

**For example**
```
array A such that:
A[0] = 4 A[1] = 1 A[2] = 3 A[3] = 2
is a permutation.

but array A such that:
A[0] = 4 A[1] = 1 A[2] = 3
is not a permutation, because value 2 is missing.
```

The goal is to check whether array A is a permutation.

**Write a function:**

`int solution(vector<int> &A);`

that, given a zero-indexed array A, returns 1 if array A is a permutation and 0 if it is not.

**For example** 
```
given array A such that:
A[0] = 4 A[1] = 1 A[2] = 3 A[3] = 2
the function should return 1.

Given array A such that:
A[0] = 4 A[1] = 1 A[2] = 3
the function should return 0.
```

**Assume that:**

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [1..1,000,000,000].
* Elements of input arrays can be modified.

**Complexity:**
* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

## Solutions

### Solution 1

* C++
```
int solution(vector<int> &A) {
    int n = A.size();
    vector<bool> bucket(n+1);
    for(int a : A)
        if(a>0 && a<=n)
            bucket[a] = true;
    for(int i=1; i<=n; ++i)
        if(bucket[i] == false) 
            return 0;
    return 1;
}
```

**Note:** 
* A permutation is a sequence containing each element from 1 to N once. 
* each element of array A is an integer within the range [1..1,000,000,000] is a miss leading information.

Remember the appared numbers in an array `bucket`. Then check the `bucket` to see if any number missing.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the input `A`.
* **worst-case space complexity:** `O(N)`, where `N` is the length of the input `A`.
