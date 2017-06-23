# 313. Super Ugly Number

### LeetCode

## Question

Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, `[1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32]` is the sequence of the first `12` super ugly numbers given primes = `[2, 7, 13, 19]` of size `4`.

**Note:**

1. 1 is a super ugly number for any given primes.
2. The given numbers in primes are in ascending order.
3. 0 < k ≤ 100, 0 < n ≤ 10<sup>6</sup>, 0 < primes[i] < 1000.
4. The nth super ugly number is guaranteed to fit in a 32-bit signed integer.

## Solutions

* C++1
```
int nthSuperUglyNumber(int n, vector<int>& primes) {
    int pn = primes.size();
    vector<int> uglys(n);
    vector<int> uglyId(pn);
    vector<int> pVal(pn, 1);
    int next = 1;
    for(int i=0; i<n; ++i)
    {
        uglys[i] = next;
        next = INT_MAX;
        for(int j=0; j<pn; ++j)
        {
            if(uglys[i] == pVal[j])
                pVal[j] = uglys[uglyId[j]++] * primes[j]; //multiply uglys from beginning
            next = min(next, pVal[j]); //update the min val
        }
    }
    return uglys[n-1];
```

## Explanation

The idea is to build up the ugly sequence from 1. Based on the primes, find the next smallest ugly number.

**e.g:**

**Input:**
```
n = 6
primes = {2, 7, 13, 19}
```
**Process:**
```
pn=4, PVal={1,1,1,1}, next=1

1. uglys[0] = 1
    pVal[0] = 1 * 2 = 2; uglyId[0] = 1; next = 2;
    pVal[1] = 1 * 7 = 7; uglyId[1] = 1; next = 2;
    pVal[2] = 1 * 13=13; uglyId[2] = 1; next = 2;
    pVal[3] = 1 * 19=19; uglyId[3] = 1; next = 2;
2. uglys[1] = 2
    pVal[0] = 2 * 2 = 4; uglyId[0] = 2; next = 4;
    next = 4;
    next = 4;
    next = 4;
3. uglys[2] = 4
    pVal[0] = 4 * 2 = 8; uglyId[0] = 3; next = 8;
    next = 7;
    next = 7;
    next = 7;
4. uglys[3] = 7
    next = 8;
    pVal[1] = 2 * 7 = 14; uglyId[1] = 2; next = 8;
    next = 8;
    next = 8;
5. uglys[4] = 8
    pVal[0] = 7 * 2 = 14; uglyId[0] = 4; next = 14;
    next = 14;
    next = 13;
    next = 13;
6. uglys[5] = 13
    next = 14;
    next = 14;
    pVal[2] = 2 * 13 = 26; uglyId[2] = 2; next = 14;
    next = 14;
.
.
.
```

**Output:**
```
13
```

* **worst-case time complexity:** O(m*n)
* **worst-case space complexity:** O(m+n)
