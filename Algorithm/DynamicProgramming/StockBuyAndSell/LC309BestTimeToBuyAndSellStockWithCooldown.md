# LC309. Best Time to Buy and Sell Stock with Cooldown

### LeetCode

## Question

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

* You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
* After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

**Example:**
```
prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
```

## Solutions

### Solution 1

* Java (7ms, 38.1MB)
```
public int maxProfit(int[] prices) {
    int n = prices.length;
    int buy[] = new int[n+1];
    int sell[] = new int[n+1];
    int cooldown[] = new int[n+1];
    buy[0] = Integer.MIN_VALUE;
    
    for(int i=1; i<=n; ++i){
        buy[i] = Math.max(cooldown[i-1]-prices[i-1], buy[i-1]);
        sell[i] = Math.max(buy[i-1]+prices[i-1], sell[i-1]);
        cooldown[i] = Math.max(Math.max(buy[i-1], sell[i-1]), cooldown[i-1]);
    }
    
    return sell[n];
}
```

The natural states for this problem is the 3 possible transactions : `buy`, `sell`, and `cooldown`. `buy` is after previous `cooldown`; `sell` is after preview `buy`; `cooldown` is after a previous `buy` or `sell`.

We can use `DP` to store the `maxProfit` of each states in each transaction.

* `buy[i`] means before day i what is the `maxProfit` for any sequence end with `buy`.
* `sell[i]` means before day i what is the `maxProfit` for any sequence end with `sell`.
* `cooldown[i]` means before day i what is the `maxProfit` for any sequence end with `cooldown`.

So, we can get:
```
buy[i] = Math.max(cooldown[i-1]-prices[i-1], buy[i-1]);
sell[i] = Math.max(buy[i-1]+prices[i-1], sell[i-1]);
cooldown[i] = Math.max(Math.max(buy[i-1], sell[i-1]), cooldown[i-1]);
```

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `prices`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `prices`.

### Solution 2

* Java (6ms, 37.9MB)
```
public int maxProfit(int[] prices) {
    int n = prices.length;
    int buy[] = new int[n+2];
    int sell[] = new int[n+2];
    buy[1] = Integer.MIN_VALUE;
    
    for(int i=2; i<=n+1; ++i){
        buy[i] = Math.max(sell[i-2]-prices[i-2], buy[i-1]);
        sell[i] = Math.max(buy[i-1]+prices[i-2], sell[i-1]);
    }
    
    return sell[n+1];
}
```

One tricky point is how do you make sure you `sell` before you `buy`, since from the equations it seems that `[buy, cooldown, buy]` is entirely possible.

In a transtraction, it must be `buy[i] <= cooldown[i] <= sell[i]`.

```
    cooldown[i] = Math.max(Math.max(buy[i-1], sell[i-1]), cooldown[i-1]);
                                    buy[i-1] <= cooldown[i-1]
->  cooldown[i] = Math.max(Math.max(cooldown[i-1], sell[i-1]), cooldown[i-1]);
->  cooldown[i] = Math.max(cooldown[i-1], sell[i-1]);
                           cooldown[i-1] <= sell[i-1]
->  cooldown[i] = sell[i-1]
```

Well, the answer lies within the fact that `buy[i-1] <= cooldown[i-1]` which means `cooldown[i] = max(sell[i-1], cooldown[i-1])`. That made sure [`buy, cooldown, buy]` is never occurred.

A further observation is that and `cooldown[i-1] <= sell[i-1]` is also true therefore `cooldown[i] = sell[i-1]`

So, we can get:
```
buy[i] = Math.max(sell[i-2]-prices[i-2], buy[i-1]);
sell[i] = Math.max(buy[i-1]+prices[i-2], sell[i-1]);
```

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `prices`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `prices`.

### Solution 3

* C++
```
int maxProfit(vector<int>& prices) {
    int buy(INT_MIN), sell(0), prev_buy(0), prev_sell(0);
    //int buy=INT_MIN, sell=0, preBuy=0, preSell=0;
    for(int price : prices)
    {
        prev_buy = buy;
        buy = max(prev_sell - price, prev_buy);
        prev_sell = sell;
        sell = max(prev_buy + price, prev_sell);
    }
    return sell;
}
```

* Java
```
public int maxProfit(int[] prices) {
    int buy = Integer.MIN_VALUE;
    int sell=0, preBuy=0, preSell=0;
    for(int price : prices)
    {
        preBuy = buy;
        buy = Math.max(preSell-price, preBuy);
        preSell = sell;
        sell = Math.max(preBuy+price, preSell);
    }
    return sell;
}
```

Since states of day i relies only on i-1 and i-2 we can reduce the O(n) space to O(1).

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `prices`.
* **worst-case space complexity:** `O(1)`

