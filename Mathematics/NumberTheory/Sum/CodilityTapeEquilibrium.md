# Codility. Tape Equilibrium

### Codility

## Question

A non-empty zero-indexed array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The difference between the two parts is the value of: |(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.

For example, consider array A such that:

`A[0] = 3 A[1] = 1 A[2] = 2 A[3] = 4 A[4] = 3`

We can split this tape in four places:

```
•	P = 1, difference = |3 − 10| = 7 
•	P = 2, difference = |4 − 9| = 5 
•	P = 3, difference = |6 − 7| = 1 
•	P = 4, difference = |10 − 3| = 7 
```

**Write a function:**

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A of N integers, returns the minimal difference that can be achieved.

For example, given:

`A[0] = 3 A[1] = 1 A[2] = 2 A[3] = 4 A[4] = 3`

the function should return 1, as explained above.

**Assume that:**

* N is an integer within the range [2..100,000];
* each element of array A is an integer within the range [−1,000..1,000].

**Complexity:**

* expected worst-case time complexity is O(N);
* expected worst-case space complexity is O(N), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++
```
#include <algorithm>
#include <climits>

int solution(vector<int> &A) {
    // write your code in C++14 (g++ 6.2.0)
    vector<int> B(A.begin(), A.end());
    int n = A.size()-1;
    for(int i=1; i<n; ++i)
    {
        A[i] += A[i-1];
        B[n-i] += B[n-i+1];
    }
    int res = INT_MAX;
    for(int i=0; i<n; ++i)
        res = min(res, abs(A[i]-B[i+1]));
    return res;
}
```

Using two array, one is to store the `left sum` of each position, one is to store the `right sum` of each position. The difference can be easily calculated by the `left sum` and the `right sum` in each position.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `A`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `A`.
