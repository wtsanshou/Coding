# LC122. Best Time to Buy and Sell Stock II

### LeetCode

## Question

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

## Solutions

### Solution 1

* C++
```
int maxProfit(vector<int>& prices) {
    int res = 0;
    for(int i=1; i<prices.size(); ++i)
        res += max(0, prices[i] - prices[i-1]);
    return res;
}
```

Many transactions make the question much easier, we just need to sum all the positive profit of each adjacent two days.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `prices`.
* **worst-case space complexity:** O(1)
