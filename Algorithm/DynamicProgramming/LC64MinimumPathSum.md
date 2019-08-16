# LC64. Minimum Path Sum

### LeetCode

## Question

Given a `m x n` grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

## Solutions

### Solution 1

* C++
```
int minPathSum(vector<vector<int>>& grid) {
    if(grid.empty()) return 0;
    int m = grid.size();
    int n = grid[0].size();
    vector<vector<int>> res(m+1, vector<int>(n+1, INT_MAX));
    res[0][1] = 0;
    for(int i=1; i<=m; ++i)
    {
        for(int j=1; j<=n; ++j)
        {
            res[i][j] = min(res[i-1][j], res[i][j-1]) + grid[i-1][j-1];
        }
    }
    return res[m][n];
}
```

* Java
```
public int minPathSum(int[][] grid) {
    int h = grid.length;
    int w = h > 0 ? grid[0].length : 0;
    if (w == 0) return 0;
    int[][] dp = new int[h + 1][w + 1];
    
    for (int i = 1; i <= h; i++) {
        dp[i][0] = Integer.MAX_VALUE;
    }
    
    for (int j = 1; j <= w; j++) {
        dp[0][j] = Integer.MAX_VALUE;
    }
    
    dp[0][1] = 0;
    
    for (int i = 1; i <= h; i++) {
        for (int j = 1; j <= w; j++) {
            dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i - 1][j - 1];
        }
    }
    
    return dp[h][w];
}
```

Using a `(m+1) x (n+1)` 2D array to store the minimizes the sum of path `res[i][j]` from `[0, 0]` to `[i, j]`

**Complexity:**

* **worst-case time complexity:** `O(m * n)`, where `m` is the height of the input `grid`, `n` is the width of the input `grid`.
* **worst-case space complexity:** `O(m * n)`, where `m` is the height of the input `grid`, `n` is the width of the input `grid`.

### Solution 2

* Java (Roll Optimize)
```
public int minPathSum(int[][] grid) {
    int h = grid.length;
    int w = h > 0 ? grid[0].length : 0;
    if (w == 0) return 0;
    int[][] dp = new int[2][w + 1];
    
    for (int j = 0; j <= w; j++) {
        dp[0][j] = Integer.MAX_VALUE;
    }
    
    dp[0][1] = 0;
    dp[1][0] = Integer.MAX_VALUE;
    
    for (int i = 1; i <= h; i++) {
        for (int j = 1; j <= w; j++) {
            dp[i % 2][j] = Math.min(dp[(i - 1) % 2][j], dp[i % 2][j - 1]) + grid[i - 1][j - 1];
        }
    }
    
    return dp[h % 2][w];
}
```

* C++
```
int minPathSum(vector<vector<int>>& grid) {
    int h = grid.size();
    int w = (h!=0) ? grid[0].size() : 0;
    if(w==0) return 0;
    vector<int> dp(w, INT_MAX);
    dp[0] = 0;
    for(int i=0; i<h; ++i)
    {
        dp[0] += grid[i][0];
        for(int j=1; j<w; ++j)
            dp[j] = min(dp[j-1], dp[j]) + grid[i][j];
    }
    return w==0 ? 0 : dp[w-1];
}
```

* Java
```
public int minPathSum(int[][] grid) {
    int m=grid.length, n=grid[0].length;
    int[] dp = new int[n];
    for(int i=1; i<n; ++i)
        dp[i] = Integer.MAX_VALUE;
    for(int i=0; i<m; ++i)
    {
        dp[0] += grid[i][0];
        for(int j=1; j<n; ++j)
            dp[j] = Math.min(dp[j], dp[j-1]) + grid[i][j];
    }
    return dp[n-1];
}
```

Only 1D array is needed to store the minimizes the sum of path.

**Complexity:**

* **worst-case time complexity:** `O(m * n)`, where `m` is the height of the input `grid`, `n` is the width of the input `grid`.
* **worst-case space complexity:** `O(n)`, where `n` is the width of the input `grid`.
