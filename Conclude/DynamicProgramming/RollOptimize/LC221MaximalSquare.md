# LC221. Maximal Square

### LeetCode

## Question

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Return 4.

## Solutions

### Solution 1

* C++1
```
int maximalSquare(vector<vector<char>>& matrix) {
    int h = matrix.size();
    int w = h>0 ? matrix[0].size() : 0;
    vector<int> dp(w+1);
    int edge=0, topLeft=0;
    for(int i=0; i<h; ++i)
    {
        for(int j=1; j<=w; ++j)
        {
            int temp = dp[j];
            if(matrix[i][j-1]=='1')
            {
                dp[j] = min(dp[j], min(dp[j-1], topLeft)) + 1;
                edge = max(edge, dp[j]);
            }
            else
                dp[j] = 0;
            topLeft = temp;
        }
    }
    return edge*edge;
}
```

## Explanation

This is a typical dynamic programming solution. 

The idea is to check topleft 'a', up 'b' and left 'c' elements, 

1. 'a', 'b', or 'c' is/are **0**: the maximum edge is 1 for current element.
2. 'a', 'b', and 'c' are all **1**: the maximum edge for current element is 1 + minimum(edge(a), edge(b), edge(c)).

**Complexity:**

* **worst-case time complexity:** O(h * w)
* **worst-case space complexity:** O(w)

### Solution 2

* Java
```
public int maxSquare(int[][] matrix) {
    int h = matrix.length;
    int w = h > 0 ? matrix[0].length : 0;
    if (w < 1) return 0;
    int[][] dp = new int[h][w];
    int maxEdge = 0;
    
    for (int i = 0; i < h; i++) {
        dp[i][0] = matrix[i][0];
        maxEdge = Math.max(maxEdge, dp[i][0]);
    }
        
    for (int j = 0; j < w; j++) {
        dp[0][j] = matrix[0][j];
        maxEdge = Math.max(maxEdge, dp[0][j]);
    }
        
    for (int i = 1; i < h; i++) {
        for (int j = 1; j < w; j++) {
            if (matrix[i][j] == 1) {
                int min = Math.min(dp[i - 1][j], dp[i][j - 1]);
                dp[i][j] = Math.min(dp[i - 1][j - 1], min) + 1;
                maxEdge = Math.max(maxEdge, dp[i][j]);
            }
        }
    }    
    
    return maxEdge * maxEdge;
}
```

**Corner cases:**

1. Empty matrix
2. `1` on the edge of the matrix.

* Java (Refactor)
```
public int maxSquare(int[][] matrix) {
    int h = matrix.length;
    int w = h > 0 ? matrix[0].length : 0;
    int[][] dp = new int[h + 1][w + 1];
    int maxEdge = 0;
        
    for (int i = 1; i <= h; i++) {
        for (int j = 1; j <= w; j++) {
            if (matrix[i - 1][j - 1] == 1) {
                int min = Math.min(dp[i - 1][j], dp[i][j - 1]);
                dp[i][j] = Math.min(dp[i - 1][j - 1], min) + 1;
                maxEdge = Math.max(maxEdge, dp[i][j]);
            } else {
                dp[i][j] = 0; // Not usefull here, but will be usefull in the Roll Optimize
            }
        }
    }    
    
    return maxEdge * maxEdge;
}
```

**State**

`dp[i][j]` is the largest square whose bottom-right index is `[i,j]`

**Function**

if `matrix[i][j] == 1`

`dp[i][j] = min(dp[i - 1][j - 1], LEFT[i][j - 1], UP[i - 1][j]) + 1`

Where LEFT[i][j - 1] means the length of the continue `1` starting from [i][j - 1] to its left;

UP[i - 1][j] means the length of the continue `1` starting from [i - 1][j] to its top;

Because `LEFT[i][j - 1] >= dp[i][j - 1]` and `UP[i - 1][j] >= dp[i - 1][j]`

So that, we can have function: `dp[i][j] = min(dp[i - 1][j - 1], dp[i][j - 1], dp[i - 1][j]) + 1`

if `matrix[i][j] == 0`, dp[i][j] = 0.

**Initialization**

* dp[i][0] = 0
* dp[0][j] = 0

**Result**

max(dp[i][j])<sup>2</sup>

**Complexity:**

* **worst-case time complexity:** `O(h * w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`.
* **worst-case space complexity:** `O(h * w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`.

### Solution 3 (Roll Optimize)

* Java
```
public int maxSquare(int[][] matrix) {
    int h = matrix.length;
    int w = h > 0 ? matrix[0].length : 0;
    int[][] dp = new int[2][w + 1];
    int maxEdge = 0;
        
    for (int i = 1; i <= h; i++) {
        for (int j = 1; j <= w; j++) {
            if (matrix[i - 1][j - 1] == 1) {
                int min = Math.min(dp[(i - 1) % 2][j], dp[i % 2][j - 1]);
                dp[i % 2][j] = Math.min(dp[(i - 1) % 2][j - 1], min) + 1;
                maxEdge = Math.max(maxEdge, dp[i % 2][j]);
            } else {
                dp[i % 2][j] = 0;
            }
        }
    }    
    
    return maxEdge * maxEdge;
}
```

**State**

`dp[i % 2][j]` is the largest square whose bottom-right index is `[i,j]`

**Function**

if `matrix[i][j] == 1`

 `dp[i % 2][j] = min(dp[(i - 1) % 2][j - 1], dp[i % 2][j - 1], dp[(i - 1) % 2][j]) + 1`

if `matrix[i][j] == 0`, dp[i % 2][j] = 0.

**Initialization**

* dp[i][0] = 0
* dp[0][j] = 0

**Result**

max(dp[i % 2][j])<sup>2</sup>

**Complexity:**

* **worst-case time complexity:** `O(h * w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`.
* **worst-case space complexity:** `O(w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`.
