# LC279. Perfect Squares

### LeetCode

## Question

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.

## Solutions

### Solution 1

* C++ (162ms)
```
int numSquares(int n) {
    vector<int> dp(n+1);
    for(int len=1; len<=n; ++len)
    {
        int minLen = INT_MAX;
        for(int i=1; i*i<=len; ++i)
            minLen = min(minLen, dp[len-i*i] + 1);
        dp[len] = minLen;
    }
    return dp[n];
}
```

* C++ (172ms)
```
int numSquares(int n) {
    vector<int> dp(n+1, INT_MAX);
    dp[0] = 0;
    for(int len=1; len<=n; ++len)
        for(int i=1; i*i<=len; ++i)
            dp[len] = min(dp[len], dp[len-i*i] + 1);
    return dp[n];
}
```

`dp[len]` means least number of perfect square numbers which sum to `len`.

`dp[len-i*i] + 1` means count the `i*i` in.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`.
* **worst-case space complexity:** `O(n)`.

### Solution 2

* C++ (306ms)
```
int numSquares(int n) {
    if(n<=0) return 0;
    vector<int> perfS(1,0);
    int len, minSN;
    while(perfS.size()<=n)
    {
        len = perfS.size();
        minSN = INT_MAX;
        for(int i=1; i*i<=len; ++i)
            minSN = min(minSN, perfS[len-i*i]+1);
        perfS.push_back(minSN);
    }
    return perfS[n];
}
```

Similar idea with **Solution 1**, but no need to initial all `dp` space at the beginning.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`.
* **worst-case space complexity:** `O(n)`.

### Solution 3

* C++ (12ms)
```
int numSquares(int n) {
    if(n<=0) return 0;
    static vector<int> perfS(1,0);
    int len, minSN;
    while(perfS.size()<=n)
    {
        len = perfS.size();
        minSN = INT_MAX;
        for(int i=1; i*i<=len; ++i)
            minSN = min(minSN, perfS[len-i*i]+1);
        perfS.push_back(minSN);
    }
    return perfS[n];
}
```

Note the number of input test cases are more than one.

Based on **Solution 2**, if we use static `dp`, we don't need to re-calculate the `dp` in the following input `n`.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`.
* **worst-case space complexity:** `O(n)`.