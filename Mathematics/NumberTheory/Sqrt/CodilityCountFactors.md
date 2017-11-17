# Codility. Count Factors

### Codility

## Question

A positive integer D is a factor of a positive integer N if there exists an integer M such that N = D * M.

For example, 6 is a factor of 24, because M = 4 satisfies the above condition (24 = 6 * 4).

Write a function:

int solution(int N);

that, given a positive integer N, returns the number of its factors.

For example, given N = 24, the function should return 8, because 24 has 8 factors, namely 1, 2, 3, 4, 6, 8, 12, 24. There are no other factors of 24.

**Assume that:**

* N is an integer within the range [1..2,147,483,647].

**Complexity:**

* expected worst-case time complexity is O(sqrt(N));
* expected worst-case space complexity is O(1).

## Solutions

* C++1
```
int solution(int N) {
    if(N==1) return 1;
    int sq = sqrt(N);
    int res = 2;
    for(int i=2; i<=sq; ++i)
    {
        if(N%i ==0) res += 2;
    }
    return (sq*sq == N) ? res-1 : res;
}
```

## Explanation

corner cases: 

1. N == 1
2. sq*sq == N

* **worst-case time complexity:** O(sqrt(N))
* **worst-case space complexity:** O(1)

# Testcase

squares  N=16, N=36

tiny  N <= 10

simple1  N=41(prime), N=42

simple2  N=69, N=64, N=120=5!

simple3  N=720=6!, N=1111

simple4  N=5,040=7!, N=12,345

simple5  N=34,879, N=40,320=8!

extreme_one  N=1

medium1  N=362,880=9!, N=1,948,102

medium2  N=3,628,800=10!, N=5,621,892, N=4,999,696

big1  N=27,043,111, N=39,916,800=11!, N = 39,992,976

big2  N=97,093,212, N=2^28

big3  N=479,001,600=12!, N=780291637(prime), N=449,991,369

extreme_maxint  N=1,000,000,000, N=MAX_INT, N=2147,395,600
