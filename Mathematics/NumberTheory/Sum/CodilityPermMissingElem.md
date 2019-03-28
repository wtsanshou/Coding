# Codility. Perm Missing Elem

### Codility

## Question

A zero-indexed array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

**Write a function:**

`int solution(vector<int> &A);`

that, given a zero-indexed array A, returns the value of the missing element.
For example, given array A such that:

`A[0] = 2 A[1] = 3 A[2] = 1 A[3] = 5`

the function should return 4, as it is the missing element.

**Assume that:**

* N is an integer within the range [0..100,000];
* the elements of A are all distinct;
* each element of array A is an integer within the range [1..(N + 1)].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(1), beyond input storage (not counting the storage required for input arguments).

**Note:**

* Elements of input arrays can be modified.
* empty list return 1

## Solutions

### Solution 1

* C++  (error from `n*(n+1)/2`, `n` could be > INT_MAX)
```
int solution(vector<int> &A) {
    // write your code in C++14 (g++ 6.2.0)
    int n = A.size()+1;
    return n*(n+1)/2 – accumulate(A.begin(), A.end(), 0);
}
```

* C++
```
int solution(vector<int> &A) {
    // write your code in C++14 (g++ 6.2.0)
    long n = A.size()+1;
    n = n*(n+1)/2;
    for(auto a : A)
        n -= a;
    return n;
}
```

The idea is to use the sum of the `[1..(N + 1)]` minus the sum of the numbers in `A`.

* **worst-case time complexity:** O(n), where `n` is the length of the `A`.
* **worst-case space complexity:** O(1)

