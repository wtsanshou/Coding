# LC121. Best Time to Buy and Sell Stock

### LeetCode

## Question

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

**Example 1:**
```
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

**Example 2:**
```
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.
```

## Solutions

### Solution 1

* C++  (8ms)
```
int maxProfit(vector<int>& prices) {
    int maxPro = 0;
    int minPrice = INT_MAX;
    for(int i = 0; i < prices.size(); i++){
        minPrice = min(minPrice, prices[i]);
        maxPro = max(maxPro, prices[i] - minPrice);
    }
    return maxPro;
}
```

Walk throug the `prices`, the maximum profit for each price is the current price minus the minimum price before it. Then compare and find the maximum profit in the `prices`.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `prices`.
* **worst-case space complexity:** O(1)

### Solution 2

* Java
```
public int solution(int[] A) {
    // write your code in Java SE 8
    int buy=Integer.MAX_VALUE;
    int sell = 0;
    for(int a : A){
        buy = Math.min(buy, a);
        sell = Math.max(sell, a-buy);
    }
    return sell;
}
```

* Java (2ms)
```
public int maxProfit(int[] prices) {
    int buy=Integer.MIN_VALUE, sell=0;
    for(int price : prices)
    {
        sell = Math.max(sell, buy+price);
        buy = Math.max(buy, -price);
    }
    return sell;
}
```

The maximum profit is the maximum sell. The goal is spending lower, selling higher.
```
sell: get money
buy: spend money
```

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `prices`.
* **worst-case space complexity:** O(1)
