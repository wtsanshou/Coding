# LC417. Pacific Atlantic Water Flow

### LeetCode

## Question

Given an `m x n` matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

**Note:**

1.	The order of returned grid coordinates does not matter.
2.	Both m and n are less than 150.

**Example:**
```
Given the following 5x5 matrix:

  Pacific ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    void dfsOceans(vector<vector<int>>& matrix, vector<vector<bool>>& visited, int i, int j, int height)
    {
        if(i<0 || i>=matrix.size() || j<0 || j>=matrix[0].size() || visited[i][j]) return;
        if(matrix[i][j] < height) return;
        visited[i][j] = true;
        dfsOceans(matrix, visited, i-1, j, matrix[i][j]);
        dfsOceans(matrix, visited, i+1, j, matrix[i][j]);
        dfsOceans(matrix, visited, i, j-1, matrix[i][j]);
        dfsOceans(matrix, visited, i, j+1, matrix[i][j]);
    }
    vector<pair<int, int>> pacificAtlantic(vector<vector<int>>& matrix) {
        vector<pair<int, int>> res;
        int h = matrix.size();
        int w = (h>0) ? matrix[0].size() : 0;
        vector<vector<bool>> Pacific(h, vector<bool>(w));
        vector<vector<bool>> Atlantic(h, vector<bool>(w));
        for(int i=0; i<h; ++i)
        {
            dfsOceans(matrix, Pacific, i, 0, matrix[i][0]);
            dfsOceans(matrix, Atlantic, i, w-1, matrix[i][w-1]);
        }
        for(int j=0; j<w; ++j)
        {
            dfsOceans(matrix, Pacific, 0, j, matrix[0][j]);
            dfsOceans(matrix, Atlantic, h-1, j, matrix[h-1][j]);
        }
        for(int i=0; i<h; ++i)
            for(int j=0; j<w; ++j)
                if(Pacific[i][j] && Atlantic[i][j])
                    res.push_back(make_pair(i, j));
        return res;
    }
};
```

DFS from each element in the 4 edges (from Pacific and Atlantic), only visit higher cells. 

If both Pacific and Atlantic can visit a cell, the cell is one in the result list.

**Complexity:**

* **worst-case time complexity:** `O(h * w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`.
* **worst-case space complexity:** `O(h * w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`.