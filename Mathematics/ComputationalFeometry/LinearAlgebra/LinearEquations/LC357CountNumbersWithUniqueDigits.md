# LC357. Count Numbers with Unique Digits

### LeetCode

## Question

Given a non-negative integer n, count all numbers with unique digits, x, where 0 ≤ x < 10<sup>n</sup>.

Example: Given n = 2, return 91. (The answer should be the total numbers in the range of 0 ≤ x < 100, excluding [11,22,33,44,55,66,77,88,99])

## Solutions

* C++1 (0ms)
```
int countNumbersWithUniqueDigits(int n) {
    n = (n>10) ? 10 : n;
    int res = 1, dig = 9, cur = 9;
    for(int i=1; i<=n; ++i)
    {
        res += cur;
        cur *= dig--;
    }
    return res;
}
```

* C++2
```
int countNumbersWithUniqueDigits(int n) {
    int dp[11] = {1};
    dp[1] = 10;
    n = min(10, n);
    for(int i=2; i<=n; ++i)
    {
        dp[i] = 9;
        int temp = 9;
        for(int j=1; j<i; ++j)
            dp[i] *= temp--;
        dp[i] += dp[i-1];
    }
    return dp[n];
}
```

* Java1
```
public int countNumbersWithUniqueDigits(int n) {
    int[] dp = new int[11];
    dp[0] = 1;
    dp[1] = 10;
    n = Math.min(n, 10);
    for(int i=2; i<=n; ++i)
    {
        dp[i] = 9;
        int temp = 9;
        for(int j=1; j<i; ++j)
            dp[i] *= temp--;
        dp[i] += dp[i-1];
    }
    return dp[n];
}
```

## Explanation

* A direct way is to use the backtracking approach.
* Backtracking should contains three states which are (the current number, number of steps to get that number and a bitmask which represent which number is marked as visited so far in the current number). Start with state (0,0,0) and count all valid number till we reach number of steps equals to 10<sup>n</sup>.
* This problem can also be solved using a dynamic programming approach and some knowledge of combinatorics.
* Let f(k) = count of numbers with unique digits with length equals k.
* f(1) = 10, ..., f(k) = 9 * 9 * 8 * ... (9 - k + 2) [The first factor is 9 because a number cannot start with 0].

```
0   1   2   3   4   5   6   7   8   9   10  11  ...

1  
    9
        9
            8
                7
                    6
                        5
                            4
                                3
                                    2
                                        1
                                            0...
```

**NOTE:** 

1. The first digit is not possible to be `0`.
2. But the second digit can be `0`.
3. If n > 10, there is no number with unique digits.

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)

