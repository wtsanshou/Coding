# LC198. House Robber

### LeetCode

## Question

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

## Solutions

### Solution 1

* C++1 (3ms)
```
int rob(vector<int>& nums) {
    int odd=0, even=0;
    for(int i=0; i<nums.size(); ++i)
    {
        if(i%2 == 0)
            odd = max(even, odd+nums[i]);
        else
            even = max(odd, even+nums[i]);
    }
    return max(odd, even);
}
```

* Java1 (1ms)
```
public int rob(int[] nums) {
    int robber1=0, robber2=0;
    for(int i=0; i<nums.length; ++i)
    {
        if(i%2==0) robber1 = Math.max(robber2, robber1+nums[i]);
        else       robber2 = Math.max(robber1, robber2+nums[i]);
    }
    return Math.max(robber1, robber2);
}
```

## Explanation

1. odd position house: max(previous even rob result, previous odd rob result + rob current house).
2. even position house: max(previous odd rob result, previous even rob result + rob current house).

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

### Solution 2

* Java
```
public long houseRobber(int[] A) {
    int n = A.length;
    if (n == 0) return 0L;
    long[] dp = new long[n + 1];
    dp[0] = 0L;
    dp[1] = A[0];
    
    for (int i = 2; i <= n; i++) {
        dp[i] = Math.max(dp[i - 1], dp[i - 2] + A[i - 1]);
    }
    
    return dp[n];
}
```

**State**

`dp[i]` is the maximum amount of money you can rob in the first `i` houses.

**Function**

`dp[i] = max(dp[i - 1], dp[i - 2] + A[i - 1]`

**Initialization**

* dp[0] = 0
* dp[1] = A[0]

**Result**

`dp[n]`

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is length of `A`.
* **worst-case space complexity:** `O(n)`, where `n` is length of `A`.

### Solution 3 (Roll Optimize)

* Java
```
public long houseRobber(int[] A) {
    int n = A.length;
    if (n == 0) return 0L;
    long[] dp = new long[2];
    dp[0] = 0L;
    dp[1] = A[0];
    
    for (int i = 2; i <= n; i++) {
        dp[i % 2] = Math.max(dp[(i - 1) % 2], dp[(i - 2) % 2] + A[i - 1]);
    }
    
    return dp[n % 2];
}
```

Based on the `Function` in the **Solution 2**, we can see the `dp[i]` is only related to `dp[i - 1]` and `dp[i - 2]`, so we can roll optimaize the `dp` to just use two variables.

**State**

`dp[i % 2]` is the maximum amount of money you can rob in the first `i` houses.

**Function**

`dp[i % 2] = max(dp[(i - 1) % 2], dp[(i - 2) % 2] + A[i - 1])`

**Initialization**

* dp[0] = 0
* dp[1] = A[0]

**Result**

`dp[n % 2]`

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is length of `A`.
* **worst-case space complexity:** `O(1)`.