# Lint440. Backpack III

### LintCode

## Question

Given n kinds of items, and each kind of item has an infinite number available. The i-th item has size A[i] and value V[i].

Also given a backpack with size m. What is the maximum value you can put into the backpack?

**Example 1:**
```
Input: 
A = [2, 3, 5, 7], V = [1, 5, 2, 4], m = 10

Output: 
15

Explanation: 
Put three item 1 (A[1] = 3, V[1] = 5) into backpack.
```

**Example 2:**
```
Input: A = 
[1, 2, 3], V = [1, 2, 3], m = 5

Output: 
5

Explanation: 
Strategy is not unique. For example, put five item 0 (A[0] = 1, V[0] = 1) into backpack.
```

**Notice**
* You cannot divide item into small pieces.
* Total size of items you put into backpack can not exceed m.

## Solutions

### Solution 1

* Java
```
public int backPackIII(int[] A, int[] V, int m) {
    int[] dp = new int[m + 1];
    
    for (int i = 0; i < A.length; i++) {
        for (int j = A[i]; j <= m; j++) {
            dp[j] = Math.max(dp[j], dp[j - A[i]] + V[i]);
        }
    }
    
    return dp[m];
}
```

Infinite Backpack use loop from small to big.

**State**

`dp[j]` is the maximum value you can put into the backpack with size `j`.

**Function**

`dp[j] = Math.max(dp[j], dp[j - A[i]] + V[i])`

where the second `dp[j]` is from `dp[i - 1][j]`. It means without the current item `A[i]`, the maximum value you can put into the backpack with size `j`; `dp[j - A[i]]` means without the current `A[i]`, the maximum value you can put into the backpack with size `j - num`, those sum plus `A[i]` could reach the target `j`.

**Initialization**

`dp[0] = 0`

 the maximum value you can put into the backpack with size with size `0` is `0`.

**Result**

`dp[m]`

**Complexity:**

* **worst-case time complexity:** `O(m)`, where `m` is the target.
* **worst-case space complexity:**  `O(m)`, where `m` is the target.
