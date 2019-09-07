# Lint. Minimum Path Sum III

### LintCode

## Question

Given a `h x w` 2D grid, find the minimum path sum from top-left to bottom-right. You can only move to `3` directions: `right`, `down`, and `right-down`.

**Exemple 1** 

```
input:
[
    [1, 1],
    [2, -1]
]

output:
0

Explanation:
1 + (-1) = 0
```

## Solutions

### Solution 1

* Java
```
public class Solution {

    public int minimumPathSumIII(int[][] grid) {
        int[] dx = {-1, 0, -1};
        int[] dy = {-1, -1, 0};
        
        int h = grid.length;
        int w = h > 0 ? grid[0].length : 0;
        
        if (w == 0) {
            return 0;
        }
        
        for (int i = 0; i < h; i++) {
            for (int j = 0; j < w; j++) {
                if (i == 0 && j == 0) {
                    continue;
                }
                int min = Integer.MAX_VALUE;
                for (int k = 0; k < 3; k++) {
                    int x = i + dx[k];
                    int y = j + dy[k];
                    if (hasPrevious(h, w, x, y)) {
                        min = Math.min(min, grid[x][y] + grid[i][j]);
                    }
                }
                grid[i][j] = min;
            }
        }
        
        return grid[h - 1][w - 1];
    }
    
    private boolean hasPrevious(int h, int w, int x, int y) {
        return x >= 0 && x < h && y >= 0 && y < w;
    }
}
```

**State**

`dp[i][j]` is the the minimum path sum from top-left to `(i, j)`.

**Function**

```
dp[i][j] = min(
                dp[i - 1][j] + grid[i][j]
                ,dp[i - 1][j - 1] + grid[i][j]
                ,dp[i][j - 1] + grid[i][j]
                )
```

**Initialization**

* dp[0][0] = grid[0][0]

**Result**

`dp[h - 1][w - 1]`

**Complexity:**

* **worst-case time complexity:** `O(h * w)`, where `h` is height of the `grid`, `w` is the width of the `grid`.
* **worst-case space complexity:** `O(1)`.
