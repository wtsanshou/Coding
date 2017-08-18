# Codility Count Semiprimes

### Codility

## Question

A prime is a positive integer X that has exactly two distinct divisors: 1 and X. The first few prime integers are 2, 3, 5, 7, 11 and 13.

A semiprime is a natural number that is the product of two (not necessarily distinct) prime numbers. The first few semiprimes are 4, 6, 9, 10, 14, 15, 21, 22, 25, 26.

You are given two non-empty zero-indexed arrays P and Q, each consisting of M integers. These arrays represent queries about the number of semiprimes within specified ranges.

Query K requires you to find the number of semiprimes within the range (P[K], Q[K]), where 1 ≤ P[K] ≤ Q[K] ≤ N.

For example, consider an integer N = 26 and arrays P, Q such that:
```
P[0] = 1 Q[0] = 26 P[1] = 4 Q[1] = 10 P[2] = 16 Q[2] = 20
```

The number of semiprimes within each of these ranges is as follows:
```
(1, 26) is 10,
(4, 10) is 4,
(16, 20) is 0.
```

**Write a function:**
```
vector<int> solution(int N, vector<int> &P, vector<int> &Q);
```

that, given an integer N and two non-empty zero-indexed arrays P and Q consisting of M integers, returns an array consisting of M elements specifying the consecutive answers to all the queries.

For example, given an integer N = 26 and arrays P, Q such that:
```
P[0] = 1 Q[0] = 26 P[1] = 4 Q[1] = 10 P[2] = 16 Q[2] = 20
```

the function should return the values [10, 4, 0], as explained above.

**Assume that:**

* N is an integer within the range [1..50,000];
* M is an integer within the range [1..30,000];
* each element of arrays P, Q is an integer within the range [1..N];
* P[i] ≤ Q[i].

**Complexity:**

* expected worst-case time complexity is O(N*log(log(N))+M);
* expected worst-case space complexity is O(N+M), beyond input storage (not counting the storage required for input arguments).

Elements of input arrays can be modified.

## Solutions

* C++1
```
bool isPrime(int n)
{
    int sq = sqrt(n);
    for(int i=2; i<=sq; ++i)
        if(n % i == 0) return false;
    return true;
}

bool isSemiPrime(int n)
{
    if(isPrime(n)) return false;
    int sq = sqrt(n);
    for(int i = sq; i>1; --i)
    {
        if(n%i == 0) 
        {
            if(isPrime(i) && isPrime(n/i)) return true;
            return false;
        }
    }
    return false;
}

vector<int> solution(int N, vector<int> &P, vector<int> &Q) {
    // write your code in C++14 (g++ 6.2.0)
    int maxP = 0;
    for(int q : Q)
        if(maxP < q) maxP = q;
    vector<int> lSemiPrimes(maxP+1);
    for(int i= 4; i<=maxP; ++i)
    {
        if(isSemiPrime(i)) lSemiPrimes[i]++;
        lSemiPrimes[i] += lSemiPrimes[i-1];
    }
    int m = Q.size();
    vector<int> res(m);
    for(int i=0; i<m; ++i)
        res[i] = lSemiPrimes[Q[i]] - lSemiPrimes[P[i]-1];
    return res;
}
```

## Testcase
```
extreme_one 
small N = 1
```

```
extreme_four 
small N = 4
```

```
small_functional 
small functional
```

```
small_random 
small random, length = ~40
```

```
medium_random 
small random, length = ~300
```

```
large_small_slices 
large with very small slices, length = ~30,000
```

```
large_random1 
large random, length = ~30,000
```

```
large_random2 
large random, length = ~30,000
```

```
extreme_large 
all max ranges
```

## Explanation

A semiprime is a natural number that is the product of two (not necessarily distinct) prime numbers. 

1. Prime number is not a semiprime. Because it only is the product of `1` and the prime number itself. `1` is not a prime.
2. `The product of two (not necessarily distinct) prime numbers` means the semiprime is **not** the product of any other than two primes. Because prime has exactly two distinct divisors: 1 and itself. i.e the semiprime can be divided by two prime. So it cannot be divided by any other numbers, except `1` and itself.


