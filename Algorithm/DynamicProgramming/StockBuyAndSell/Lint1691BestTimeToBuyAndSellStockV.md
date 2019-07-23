# Lint1691. Best Time to Buy and Sell Stock V

### LintCode

## Question

Given a stock n-day price, you can only trade at most once a day, you can choose to buy a stock or sell a stock or give up the trade today, output the maximum profit can reach.

**Example 1:**

```
Input:
[1,2,10,9]

Output:
16

Explanation:
you can buy in day 1,2 and sell in 3,4.
profit:-1-2+10+9 = 16 
```

**Example 2:**

```
Input:
[9,5,9,10,5]

Output:
5

Explanation:
you can buy in day 2 and sell in 4.
profit:-5 + 10 = 5
```

**Notice**

* 1 ≤ n ≤ 10000

## Solutions

### Solution 1

```
public int maxProfit(int[] prices) {
    int n = prices.length;
    int[][] dp = new int[n][n];

    for (int period = 1; period < n; period++) {
        for (int left = 0; left < n - period; left++) {
            int right = left + period;
            dp[left][right] = dp[left + 1][right - 1] + prices[right] - prices[left];
            for (int mid = left + 1; mid <= right; mid++) {
                dp[left][right] = Math.max(dp[left][mid - 1] + dp[mid][right], dp[left][right]);
            }
        }
    }

    return dp[0][n - 1];
}
```

First, some requirements need to be clearify:

1. Only trade `at most` once a day.
2. `at most` one stock per trade.
3. You don't need to sell your stock before you buy. In other word, you can keep more than one stock.

I didn't realize this is a DP question at the beginning. Then I found the result could be many possible combbinations. This really like a DP question.

To figure out the DP solution, we need to divide the problem to some smaller sub problems. The most simple way is to cut the problem to two pieces of sub problems. So the formula is `dp[i][j] = dp[i][mid-1] + dp[mid][j]`. But this formula does not cover all scenarios. 

One scenario is to buy at day `i` and sell at day `j` plus `dp[i+1][j-1]`. Because `dp[i+1][j-1]` is already know, we just need to calculate it once.

I don't have enough test cases to verify the correctness of the solution, but the main logic is right.

**Complexity:**

* **worst-case time complexity:** O(n<sup>3</sup>), where `n` is the length of the input `prices`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of the input `prices`.
