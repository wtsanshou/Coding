# Codility. Common Prime Divisors

### Codility

## Question

A prime is a positive integer X that has exactly two distinct divisors: 1 and X. The first few prime integers are 2, 3, 5, 7, 11 and 13.

A prime D is called a prime divisor of a positive integer P if there exists a positive integer K such that D * K = P. For example, 2 and 5 are prime divisors of 20.

You are given two positive integers N and M. The goal is to check whether the sets of prime divisors of integers N and M are exactly the same.

**For example, given:**

* N = 15 and M = 75, the prime divisors are the same: {3, 5};
* N = 10 and M = 30, the prime divisors aren't the same: {2, 5} is not equal to {2, 3, 5};
* N = 9 and M = 5, the prime divisors aren't the same: {3} is not equal to {5}.

**Write a function:**

`int solution(vector<int> &A, vector<int> &B);`

that, given two non-empty zero-indexed arrays A and B of Z integers, returns the number of positions K for which the prime divisors of A[K] and B[K] are exactly the same.

For example, given:

`A[0] = 15 B[0] = 75 A[1] = 10 B[1] = 30 A[2] = 3 B[2] = 5`

the function should return 1, because only one pair (15, 75) has the same set of prime divisors.

**Assume that:**

* Z is an integer within the range [1..6,000];
* each element of arrays A, B is an integer within the range [1..2,147,483,647].

**Complexity:**

* expected worst-case time complexity is O(Z*log(max(A)+max(B))<sup>2</sup>);
* expected worst-case space complexity is O(1), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
int GCD(int A, int B)
{
    return B==0 ? A : GCD(B, A%B);
}

int divideByGCD(int A, int gcd)
{
    int c = GCD(A, gcd);
    return (c==1) ? A : divideByGCD(A/c, gcd);
}

bool hasSamePrimeDivisort(int A, int B)
{
    int gcd = GCD(A, B);
    int a = divideByGCD(A, gcd);
    int b = divideByGCD(B, gcd);
    return a==1 && b==1;
}

int solution(vector<int> &A, vector<int> &B) {
    int res = 0;
    for(unsigned int i=0; i<A.size(); ++i)
        if(hasSamePrimeDivisort(A[i], B[i]))
            res++;
    return res;
}
```

## Explanation

<a href="https://en.wikipedia.org/wiki/Greatest_common_divisor">Greatest Common Divisor (GCD)</a>

? 

## Testcase

extreme  extreme test with small values

simple_1  simple test with small values

simple_2  simple test with small values

primes  powers of primes

small_primes  small primes

small_all_pairs  all pairs 1-10, length = 100

small_random  small random test, length = 100

large_all_pairs  all pairs 1-70, length = ~5,000

large_random  large random tests, length = ~6,000

many_factors  factorial test

many_factors2  factorial test

big_powers  powers of 2 and 3

extreme_maximal  extreme test with maximal values

