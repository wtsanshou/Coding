# LC1687. Pave Square

### LintCode (Easy)

## Question

In a rectangular square of `2×n`, a `1×2` domino is used to pave the square. Input n and return the total number of paving schemes.

**Example 1:**

```
Input:
2

Output:
2

Explanation:
Use two 1*2 or two 2*1 dominos.
```

**Example 2:**

```
Input:
3

Output:
3

Explanation:
Use three 1*2 or three 2*1 dominos.
```

**Notice**

* 1 ≤ n ≤ 50

## Solutions

### Solution 1

* Java
```
public long getTotalSchemes(int n) {
    long[] dp = new long[51];
    dp[1] = 1L;
    dp[2] = 2L;
    
    for (int i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    
    return dp[n];
}
```

This quesiton is just like the question `Climbing stair`. Typical DP problem.

**State**

`dp[i]` is the total schemes in a rectangular square of `2×i`.

**Function**

`dp[i] = dp[i - 1] + dp[i - 2];`

**Initialization**

* dp[1] = 1L
* dp[2] = 2L

**Result**

`dp[n]`

**Note** Schemes number could be huge, so do not forget to use `long`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the width of the rectangular square.
* **worst-case space complexity:** `O(n)`, where `n` is the width of the rectangular square.

### Solution 2

* Java
```
public long getTotalSchemes(int n) {
    long[] dp = new long[3];
    dp[1] = 1L;
    dp[2] = 2L;
    
    for (int i = 3; i <= n; i++) {
        dp[i % 3] = dp[(i - 1) % 3] + dp[(i - 2) % 3];
    }
    
    return dp[n % 3];
}
```

The `Roll Optimize` version of the **Solution 1**.


* **worst-case time complexity:** `O(n)`, where `n` is the width of the rectangular square.
* **worst-case space complexity:** `O(1)`.
