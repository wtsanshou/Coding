# LC714. Best Time to Buy and Sell Stock with Transaction Fee

### LeetCode

## Question

Your are given an array of integers prices, for which the i-th element is the price of a given stock on day i; and a non-negative integer fee representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time (ie. you must sell the stock share before you buy again.)

Return the maximum profit you can make.

**Example 1:**
```
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
```

**Explanation:**
```
The maximum profit can be achieved by:
Buying at prices[0] = 1
Selling at prices[3] = 8
Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
```

**Note:**

* 0 < prices.length <= 50000.
* 0 < prices[i] < 50000.
* 0 <= fee < 50000.


* Java1 (Time Limit Exceeded) 
```
public int maxProfit(int[] prices, int fee) {
    int n = prices.length;
    int [][] dp = new int[n][n];
    for(int j=1; j<n; ++j){
        for(int i=j-1; i>=0; --i){
            dp[i][j] = Math.max(0, prices[j] - prices[i] - fee);
            for(int m=i; m<j; ++m)
                dp[i][j] = Math.max(dp[i][j], dp[i][m] + dp[m+1][j]);
        }
    }
    return dp[0][n-1];
}
```

* java2 
```
public int maxProfit(int[] prices, int fee) {
    int cash=0, hold=-prices[0];
    for(int i=1; i<prices.length; ++i){
        cash = Math.max(cash, hold+prices[i]-fee);
        hold = Math.max(hold, cash-prices[i]); //max(have bought, buy now)
    }
    return cash;
}
```

## Explanation

**Solution 1** 

It is Time Limit Exceeded. The idea is using dynamic programming to get the max profit of every subarray.

* **worst-case time complexity:** O(n<sup>3</sup>)
* **worst-case space complexity:** O(n<sup>2</sup>)

**Solution 2** 

At the end of i<sup>th</sup> day, 

1. If we don't have a share, the maxmimum `cash` we can have.
2. If we have a share, the maximum `hold` we can have. 

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

