# LC322. Coin Change

### LeetCode

## Question

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

**Example 1:**

```
coins = [1, 2, 5], amount = 11
return 3 (11 = 5 + 5 + 1)
```

**Example 2:**

```
coins = [2], amount = 3
return -1.
```

**Note:**

You may assume that you have an infinite number of each kind of coin.

## Solutions

### Solution 1

* C++ (TLE)
```
int coinChange(vector<int>& coins, int amount) {
    if(amount==0) return 0;
    int res = INT_MAX;
    for(int coin : coins)
    {
        if(amount-coin >= 0)
        {
            int x = coinChange(coins, amount-coin);
            if(x!=-1)
                res = min(res, x) + 1;
        }
    }
    return res==INT_MAX ? -1 : res;
}
```

Using recursive, each time use one coin and then recurse down.

**Complexity:**

* **worst-case time complexity:** O(n<sup>m</sup>), where `n` is the number of `coins`, `m` is the `amount`.
* **worst-case space complexity:** `O(m)`, where `m` is the `amount`.

### Solution 2

* C++ (TLE)
```
int coinChange(vector<int>& coins, int amount) {
    if(amount == 0) return 0;
    vector<int>dp(amount+1, INT_MAX);
    for (int coin : coins)
        if (coin <= amount)
            dp[coin] = 1;
    for (int i = 1; i <= amount; ++i)
    {
        if (dp[i] == 1) continue;
        for (int j = i-1; j >= 1; --j)
            if (dp[j] != INT_MAX && dp[i-j] != INT_MAX) 
                dp[i] = min(dp[i], dp[j] + dp[i - j]);
    }
    return dp[amount] == INT_MAX ? -1 : dp[amount];
}
```

Using `dp[i]` to represent the fewest number of coins that you need to make up the amount `i`.

**Complexity:**

* **worst-case time complexity:** O(m<sup>2</sup>), where `m` is the `amount`.
* **worst-case space complexity:** `O(m)`, where `m` is the `amount`.

### Solution 3

* C++
```
int coinChange(vector<int>& coins, int amount) {
    vector<int>dp(amount+1, amount+1);
    dp[0] = 0;
    for(int coin : coins)
        for(int i=coin; i<=amount; ++i)
            dp[i] = min(dp[i], dp[i-coin]+1);
    return dp[amount]>amount ? -1 : dp[amount];
}
```

* Java
```
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);
    dp[0] = 0;
    
    for (int coin : coins) {
        for (int i = coin; i <= amount; i++) {
            dp[i] = Math.min(dp[i], dp[i - coin] + 1);
        }
    }
    
    return dp[amount] > amount ? -1 : dp[amount];
}
```

We don't need to check every amount from `0` to `amount`. we just need to check from each `coin` to `amount`.

**Complexity:**

* **worst-case time complexity:** `O(m * n)`, where `n` is the number of `coins`, `m` is the `amount`.
* **worst-case space complexity:** `O(m)`, where `m` is the `amount`.
