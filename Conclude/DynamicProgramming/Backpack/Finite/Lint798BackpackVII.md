# Lint798. Backpack VII

### LintCode (Medium)

## Question

Assume that you have n yuan. There are many kinds of rice in the supermarket. Each kind of rice is bagged and must be purchased in the whole bag. Given the weight, price and quantity of each type of rice, find the maximum weight of rice that you can purchase.

**Example 1:**
```
Input:  
n = 8, prices = [3,2], weights = [300,160], amounts = [1,6]

Output:  
640

Explanation:  
Buy the second rice(price = 2) use all 8 money.
```

**Example 2:**
```
Input:  
n = 8, prices  = [2,4], weight = [100,100], amounts = [4,2 ]

Output:  
400    

Explanation:  
Buy the first rice(price = 2) use all 8 money.
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param n: the money of you
     * @param prices: the price of rice[i]
     * @param weight: the weight of rice[i]
     * @param amounts: the amount of rice[i]
     * @return: the maximum weight
     */
    public int backPackVII(int n, int[] prices, int[] weight, int[] amounts) {
        int max = 0;
        for (int i = 0; i < prices.length; i++)
            max = Math.max(max, dfs(n, prices, weight, amounts, i, 0));
            
        return max;
    }
    
    private int dfs(int n, int[] prices, int[] weight, int[] amounts, int ithBag, int totalAmount) {
        if (ithBag >= prices.length) {
            if (n >= 0)
                return totalAmount;
        }
        
        int max = 0; 
        
        for (int i = ithBag; i < prices.length; i++) {
            for (int j = 0; j <= amounts[i]; j++) {
                if (n - (j * prices[i]) >= 0)
                    max = Math.max(max, dfs(n - (j * prices[i]), prices, weight, amounts, i + 1, totalAmount + (j * weight[i])));
            }
        }
        
        return max;
    }
}
```

This is Backpack question, I know it can be done by `DP`.

But, this question has too many parameters. So I first came out the `DFS` solution to clear my mind.

The idea is to search starting from each kind of rice. Try every amount of this kind of rice and remember it in the `totalAmount`.

The exit point is the end of all kinds of rices. 

**NOTE** make sure `balance` (`n`) is enough to purchase rick.

**Complexity:**

* **worst-case time complexity:** O(a<sup>m</sup>), where `m` is the length of the input `prices`, `a` is the maximum value in `amount`.
* **worst-case space complexity:** `O(m)`, where `m` is the length of the input `prices`.

### Solution 2

* Java

```
public class Solution {
    /**
     * @param n: the money of you
     * @param prices: the price of rice[i]
     * @param weight: the weight of rice[i]
     * @param amounts: the amount of rice[i]
     * @return: the maximum weight
     */
    public int backPackVII(int n, int[] prices, int[] weight, int[] amounts) {
        int max = 0;
        int m = prices.length;
        int[][] mem = new int[m][n + 1];
        for (int i = 0; i < prices.length; i++)
            max = Math.max(max, dfs(n, prices, weight, amounts, i, 0, mem));
            
        return max;
    }
    
    private int dfs(int n, int[] prices, int[] weight, int[] amounts, int ithBag, int totalAmount, int[][] mem) {
        if (ithBag >= prices.length) {
            if (n >= 0)
                return totalAmount;
        }
        
        if (mem[ithBag][n] > 0) return mem[ithBag][n];
        int max = 0; 
        
        for (int i = ithBag; i < prices.length; i++) {
            for (int j = 0; j <= amounts[i]; j++) {
                if (n - (j * prices[i]) >= 0) {
                    max = Math.max(max,  totalAmount + (j * weight[i]) + dfs(n - (j * prices[i]), prices, weight, amounts, i + 1, 0 , mem));
                }
            }
        }
        mem[ithBag][n] = max;
        return max;
    }
}
```

Based on **Solution 1**, we can see there are many duplicate `DFS`. In this case we can use `DP`. First, we can think of using `Memory search` to remember the result of the duplicate `DFS`. 

**State**

`dp[i][j]` is the maximum amount of purchased rices starting from i<sup>th</sup> rice with `j` balance.

**NOTE** here we need to take the `totalAmount + (j * weight[i])` out of the `DFS` to be useful for `Memory search`.

`totalAmount` is not usefull anymore, so a refactor version is:

* java
```
public class Solution {
    /**
     * @param n: the money of you
     * @param prices: the price of rice[i]
     * @param weight: the weight of rice[i]
     * @param amounts: the amount of rice[i]
     * @return: the maximum weight
     */
    public int backPackVII(int n, int[] prices, int[] weight, int[] amounts) {
        // write your code here
        int max = 0;
        int m = prices.length;
        int[][] mem = new int[m][n + 1];
        for (int i = 0; i < prices.length; i++)
            max = Math.max(max, dfs(n, prices, weight, amounts, i, mem));
            
        return max;
    }
    
    private int dfs(int n, int[] prices, int[] weight, int[] amounts, int ithBag, int[][] mem) {
        if (ithBag >= prices.length) {
                return 0;
        }
        
        if (mem[ithBag][n] > 0) return mem[ithBag][n];
        int max = 0; 
        
        for (int i = ithBag; i < prices.length; i++) {
            for (int j = 0; j <= amounts[i]; j++) {
                if (n - (j * prices[i]) >= 0) {
                    max = Math.max(max,  (j * weight[i]) + dfs(n - (j * prices[i]), prices, weight, amounts, i + 1 , mem));
                }
            }
        }
        mem[ithBag][n] = max;
        return max;
    }
}
```

**Complexity:**

* **worst-case time complexity:** Difficult to know.
* **worst-case space complexity:** `O(m * n)`, where `m` is the length of the input `prices`, `n` is the balance.

### Solution 3

* Java
```
public int backPackVII(int n, int[] prices, int[] weight, int[] amounts) {
    int max = 0;
    int m = prices.length;
    int[][] dp = new int[m][n + 1];

    for (int i = 0; i <= n; i++) {
        int count = i / prices[0];
        if (count <= amounts[0])
            dp[0][i] = count * weight[0];
        else if (i > 0)
            dp[0][i] = dp[0][i - 1];
    }
    
    for (int i = 1; i < prices.length; i++) {
        for (int ta = amounts[i]; ta >= 0; ta--) {
            for (int j = n; j >= ta * prices[i]; j--) {
                dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - ta * prices[i]] + ta * weight[i]);
                max = Math.max(max, dp[i][j]);
            }
        }
    }

    return max;
}
```

Finally, we get the `DP` version.

**State**

`dp[i][j]` is the the maximum amount of purchased rices in the range [0, i] rice with `j` balance.

**Function**

`dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - ta * prices[i]] + ta * weight[i])`

**Initialization**

`dp[0][i] = count * weight[0]`

NOTE: The limit of `amount[0]` and `balance` may not equal to `count * prices[0]`

**Result**

`max(dp[i][j])`

**Complexity:**

* **worst-case time complexity:** `O(n * m * a)`, where `m` is the length of the input `prices`, `a` is the maximum value in `amount`, `n` is the balance.
* **worst-case space complexity:**  `O(n * m)`, where `m` is the length of the input `prices`, `n` is the balance.

### Solution 4 (Roll Optimize)

* Java
```
public int backPackVII(int n, int[] prices, int[] weight, int[] amounts) {
        int max = 0;
        int[][] dp = new int[2][n + 1];
        for (int i = 0; i <= n; i++) {
            int count = i / prices[0];
            if (count <= amounts[0])
                dp[0][i] = count * weight[0];
            else if (i > 0)
                dp[0][i] = dp[0][i - 1];
        }
        
        for (int i = 1; i < prices.length; i++) {
            for (int ta = amounts[i]; ta >= 0; ta--) {
                for (int j = n; j >= ta * prices[i]; j--) {
                    dp[i % 2][j] = Math.max(dp[i % 2][j], dp[(i - 1) % 2][j - ta * prices[i]] + ta * weight[i]);
                    max = Math.max(max, dp[i % 2][j]);
                }
            }
        }
        return max;
    }
```

**Function**

```
dp[i][j] = Math.max(dp[i][j], dp[i - 1][j - ta * prices[i]] + ta * weight[i])
        ||
        ||
        \/
dp[i % 2][j] = Math.max(dp[i % 2][j], dp[(i - 1) % 2][j - ta * prices[i]] + ta * weight[i])
```

**Complexity:**

* **worst-case time complexity:** `O(n * m * a)`, where `m` is the length of the input `prices`, `a` is the maximum value in `amount`, `n` is the balance.
* **worst-case space complexity:**  `O(n)`, where `n` is the balance.
