# Codility. Passing Cars

### Codility

## Question

A non-empty zero-indexed array A consisting of N integers is given. The consecutive elements of array A represent consecutive cars on a road.

Array A contains only 0s and/or 1s:

* 0 represents a car traveling east,
* 1 represents a car traveling west.

The goal is to count passing cars. We say that a pair of cars (P, Q), where 0 ≤ P < Q < N, is passing when P is traveling to the east and Q is traveling to the west.

For example, consider array A such that:

`A[0] = 0 A[1] = 1 A[2] = 0 A[3] = 1 A[4] = 1`

We have five pairs of passing cars: (0, 1), (0, 3), (0, 4), (2, 3), (2, 4).

**Write a function:**

`int solution(vector<int> &A);`

that, given a non-empty zero-indexed array A of N integers, returns the number of pairs of passing cars.

The function should return −1 if the number of pairs of passing cars exceeds 1,000,000,000.

For example, given:

`A[0] = 0 A[1] = 1 A[2] = 0 A[3] = 1 A[4] = 1`

the function should return 5, as explained above.

**Assume that:**

* N is an integer within the range [1..100,000];
* each element of array A is an integer that can have one of the following values: 0, 1.

Elements of input arrays can be modified.

## Solutions

* C++
```
int solution(vector<int> &A) {
    int n = A.size()-1;
    for(int i=n, count=0; i>0; --i)
        if(A[i]==1) A[i] = ++count;
    int res = 0;
    for(int i=0, num0=1; i<n; ++i)
    {
        if(A[i]==0 && A[i+1]>0)
        {
            int pre = res;
            res += num0*A[i+1];
            if(res>1000000000 || (res-pre)/num0 != A[i+1]) return -1;
        }
        else if(A[i]==0) num0++;
        else num0 = 1;
    }
    return res;
}
```

* C++
```
int solution(vector<int> &A) {
    int n = A.size()-1;
    for(int i=n, count=0; i>0; --i)
        if(A[i]==1) A[i] = ++count;
    long res = 0;
    for(int i=0, num0=1; i<n; ++i)
    {
        if(A[i]==0 && A[i+1]>0)
        {
            res += (long)num0*A[i+1];
            if(res>1000000000) return -1;
        }
        else if(A[i]==0) num0++;
        else num0 = 1;
    }
    return res;
}
```

1. From right to left of `A`, at the position of cars `A[i]` who traveling west (`A[i] == 1`), cout the number of cars who are east of the car `A[i]` and also travling west.
2. From left to right, count the number `num0` of continuous cars who are travling east (`A[i] == 0`). Add `num0` times the first `A[i+1] > 0` who is the number of cars travling west to the final result.

**Complexity:**

* expected worst-case time complexity is `O(N)`, where `N` is the number of the cars `A`.
* expected worst-case space complexity is `O(1)`, beyond input storage (not counting the storage required for input arguments).

## Testcase

single 

single element



double 

two elements


simple 

simple test


small_random 

random, length = 100


small_random2 

random, length = 1000


medium_random 

random, length = ~10,000


large_random 

random, length = ~100,000


large_big_answer 

0..01..1, length = ~100,000


large_alternate 

0101..01, length = ~100,000


large_extreme 

large test with all 1s/0s, length = ~100,000

