# LC695. Max Area of Island

### LeetCode

## Question

Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

**Example 1:**
```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.

**Example 2:**
```
[[0,0,0,0,0,0,0,0]]
```

Given the above grid, return 0.

**Note:** The length of each dimension in the given grid does not exceed 50.

## Solutions

* C++1
```
class Solution {
public:
    int dfs(vector<vector<int>>& grid, int i, int j){
        if(i<0 || j<0 || i>=grid.size() || j>=grid[0].size() || grid[i][j]==0) return 0;
        grid[i][j] = 0;
        return 1 + dfs(grid, i-1, j) + dfs(grid, i+1, j) + dfs(grid, i, j-1) + dfs(grid, i, j+1);
    }
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int h = grid.size();
        int w = h>0 ? grid[0].size() : 0;
        int res = 0;
        for(int i=0; i<h; ++i)
            for(int j=0; j<w; ++j)
                if(grid[i][j] == 1)
                    res = max(res, dfs(grid, i, j));
        return res;
    }
};
```

* Python
```
class Solution:
    
    IJ = [(0, -1), (-1, 0),  (0, 1), (1, 0)]
    
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        result = 0
        row = len(grid)
        col = len(grid[0]) if row > 0 else 0
        for i in range(row):
            for j in range(col):
                if grid[i][j] == 1:
                    result = max(result, self.check_island_size(grid, i, j, row, col))
        return result
    
    def check_island_size(self, grid: List[List[int]], i: int, j: int, row: int, col: int) -> int:
        result = 1
        grid[i][j] = 0
        for x, y in self.IJ:
            a, b = i + x, j + y
            if 0 <= a < row and 0 <= b < col and grid[a][b] == 1:
                result += self.check_island_size(grid, a, b, row, col)
        
        return result
```

## Explanation

Use DFS to count the area of each island in the given 2D array.

* **worst-case time complexity:** O(m * n)
* **worst-case space complexity:** O(m * n)

