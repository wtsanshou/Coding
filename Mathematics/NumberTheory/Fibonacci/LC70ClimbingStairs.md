# LC70. Climbing Stairs

### LeetCode

## Question

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given n will be a positive integer.

## Solutions

### Solution 1

* C++1 (0ms)
```
int climbStairs(int n) {
    if(n<2) return 1;
    int f1=1, f2=1, res=0;
    for(int i=2;i<=n;i++)
    {
        res = f1+f2;
        f1=f2;
        f2=res;
    }
    return res;
}
```

* Java1 (TLE)
```
public int climbStairs(int n) {
    if(n<2) return 1;
    else if(n==2) return 2;
    else return climbStairs(n-1) + climbStairs(n-2);
}
```

## Explanation

Recursive method is easier to understand and save some lines of code, but will consume a lot of duplicated calculation.

**Complexity:**

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

### Solution 2

* Java
```
public int climbStairs(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    int[] dp = new int[n + 1];
    dp[0] = 1;
    dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2];
    return dp[n];
}
```

**State**

`dp[i]` is the distinct ways you can climb to the stair `i`.

**Function**

`dp[i] = dp[i - 1] + dp[i - 2]`

**Initialization**

* dp[0] = 1
* dp[1] = 1

**Result**

`dp[n]`

**Complexity:**

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)

### Solution 3 (Roll Optimize)

* Java
```
public int climbStairs(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    int[] dp = new int[2];
    dp[0] = 1;
    dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i % 2] = dp[(i - 1) % 2] + dp[(i - 2) % 2];
    return dp[n % 2];
}
```

Based on the `Function` in the **Solution 2**, we can see the `dp[i]` is only related to `dp[i - 1]` and `dp[i - 2]`, so we can roll optimaize the `dp` to just use two variables.

**State**

`dp[i % 2]` is the distinct ways you can climb to the stair `i`.

**Function**

`dp[i % 2] = dp[(i - 1) % 2] + dp[(i - 2) % 2]`

**Initialization**

* dp[0] = 1
* dp[1] = 1

**Result**

`dp[n % 2]`

**Complexity:**

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)
