# LC62. Unique Paths

### LeetCode

## Question

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![LC62 Unique Paths](Images/LC62UniquePaths.png)

Above is a 3 x 7 grid. How many possible unique paths are there?

Note: m and n will be at most 100.

## Solutions

* C++1 (0ms) O(m*n)
```
int uniquePaths(int m, int n) {
    if(n<1) return 0;
    vector<int> dp(n, 1);
    for(int i=1; i<m; ++i)
        for(int j=1; j<n; ++j)
            dp[j] += dp[j-1]; 
    return dp[n-1];
}
```

* C++2
```
int uniquePaths(int m, int n) {
    if(m>n) return uniquePaths(n, m);
    double res=1;
    for(int i=m-1; i>0; --i)
    {
        res *= (double)(n-1+i)/i;
    }
    return round(res);
}
```

* Java1
```
public int uniquePaths(int m, int n) {
    if(m < n)
        return uniquePaths(n, m);
    if( n<= 0) return 0;
    int[] dp = new int[n];
    Arrays.fill(dp, 1);
    for(int i=1; i<m; ++i)
        for(int j=1; j<n; ++j)
            dp[j] += dp[j-1];
    return dp[n-1];
}
```

## Explanation

For each point, at most two moving sourses (left and top). So the possible unique paths are `left + top`.

The most direct way is using a 2D array top store the possible unique paths of each point from top-left to bottom-right.

Here we can just use a 1D array to store the possible unique paths of each point, because we calculate `row by row` or `column by column`.

**NOTE:** select `min(row, column` may save some memory.

* **worst-case time complexity:** O(m * n)
* **worst-case space complexity:** O(min(m, n))
