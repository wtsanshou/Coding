# Lint92. Backpack

### LintCode

## Question

Given n items with size Ai, an integer m denotes the size of a backpack. How full you can fill this backpack?

**Example 1:**
```
	Input:  [3,4,8,5], backpack size=10
	Output:  9
```

**Example 2:**
```
	Input:  [2,3,5,7], backpack size=12
	Output:  12
```

**Challenge**

* O(n x m) time and O(m) memory.
* O(n x m) memory is also acceptable if you do not know how to optimize memory.

**Notice**

* You can not divide any item into small pieces.

## Solutions

### Solution 1

* Java (Time Limit Exceeded)
```
public class Solution {
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    public int backPack(int m, int[] A) {
        return dfs(m, A, 0, 0);
    }
    
    private int dfs(int m, int[] A, int start, int sum) {
        if (start >= A.length) {
            if (sum <= m) return sum;
            return 0;
        }
        
        int res = Integer.MIN_VALUE;
        for (int i = start; i < A.length; i++) {
            if (sum + A[i] <= m) {
                res = Math.max(res, sum + A[i]);
                res = Math.max(res, dfs(m, A, i + 1, sum + A[i]));
            }
        }
        
        return res;
    }
}
```

At the beginning, I had a feeling that this is a DP problem. The **Challenge** gave me some clue. But it's not easy to get DP solution directly in a short time. So I tried the brute force solution first. 

The idea is to use `DFS` starting from each element in the array `A`. I am using `0` as the initial value of the result, although the question does not say the size is non-negative. We can assume size must be non-negative value. 

Sarting from each element in the array `A`, only `sum + A[i] <= m` could possible be combined to generate the result. We want the reslut is the maximum value which is less than or equals to target `m`.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the number of `A`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of `A`.


### Solution 2

* Java
```
public int backPack(int m, int[] A) {
    int n = A.length;
    int[][] dp = new int[n + 1][m + 1];
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (A[i - 1] > j)
                dp[i][j] = dp[i - 1][j];
            else
                dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - A[i - 1]] + A[i - 1]);
        }
    }
    
    return dp[n][m];
}
```

Based on the clue from **Challenge**, there must be a nested loop. One is `n loop`, one is `m loop`.

To use `DP`, we must break the question down to small sub questions. If we use dp[n][m] as the final result, we can assum dp[n - 1] has already known. 

What is the meaning of dp[i][j]? Based on **Solution 1**, we can have the idea that `i` is [0, i) elements in the `A`, `j` is the target of the `i` elements.

1. If `A[i - 1] > j`, `A[i - 1]` is not possible in the `dp[i][j]`, so `dp[i][j] = dp[i - 1][j]`.
2. Else, `dp[i][j]` could be dp[i - 1][j], or A[i - 1] + `dp[i - 1][j - A[i - 1]]` (maximum backpack to target `j - A[i - 1]` from elements range `[0, i - 1)`). The larger one will be put in `dp[i][j]`.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the number of `A`.
* **worst-case space complexity:**  `O(n * m)`, where `n` is the number of `A`.

### Solution 3

* Java (Roll Optimize)
```
public int backPack(int m, int[] A) {
    int n = A.length;
    int[][] dp = new int[2][m + 1];
    
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (A[i - 1] > j) {
                dp[i % 2][j] = dp[(i - 1) % 2][j];
                continue;
            }
            dp[i % 2][j] = Math.max(dp[(i - 1) % 2][j], dp[(i - 1) % 2][j - A[i - 1]] + A[i - 1]);
            
        }
    }
    
    return dp[n % 2][m];
}
```

* Java
```
public int backPack(int m, int[] A) {
    int n = A.length;
    int[] dp = new int[m + 1];
    int[] preDP = new int[m + 1];
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (A[i - 1] > j) 
                dp[j] = preDP[j];
            else
                dp[j] = Math.max(preDP[j], preDP[j - A[i - 1]] + A[i - 1]);
        }
        preDP = Arrays.copyOfRange(dp, 0, m + 1);
    }
    return dp[m];
}
```

Based on **Solution 2**, we can see that only `dp[i - 1]` need to be remembered. So we can use a `preDP` to always remember the previous `dp`. The rest is the same as **Solution 2**.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the number of `A`.
* **worst-case space complexity:**  `O(m)`.

### Solution 4 (Dimensionality Reduction)

* Java
```
public int backPack(int m, int[] A) {
    int[] dp = new int[m + 1];
        
    for (int a : A) {
        for (int i = m; i >= a; i--) {
            dp[i] = Math.max(dp[i], dp[i- a] + a);
        }
    }
    
    return dp[m];
}
```

For finite number of element, we can reduce the dimension. In this case, the second loop should search from big value (`m`) to small value (`a`).

**State**

`dp[i]` is the maximum sum size of items with backpack size `i`.

**Function**

`dp[i] = max(dp[i], dp[i - A[i]] + A[i])`

**Initialization**


**Result**

`dp[m]`

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the number of `A`.
* **worst-case space complexity:**  `O(m)`.

