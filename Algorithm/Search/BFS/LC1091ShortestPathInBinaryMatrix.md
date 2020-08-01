# LC1091. Shortest Path in Binary Matrix

### LeetCode

## Question

In an N by N square grid, each cell is either empty (0) or blocked (1).

A clear path from top-left to bottom-right has length k if and only if it is composed of cells C_1, C_2, ..., C_k such that:

Adjacent cells C_i and C_{i+1} are connected 8-directionally (ie., they are different and share an edge or corner)

C_1 is at location (0, 0) (ie. has value grid[0][0])

C_k is at location (N-1, N-1) (ie. has value grid[N-1][N-1])

If C_i is located at (r, c), then grid[r][c] is empty (ie. grid[r][c] == 0).

Return the length of the shortest such clear path from top-left to bottom-right. If such a path does not exist, return -1.

**Example 1:**
```
Input: [[0,1],[1,0]]

Output: 2
```

**Example 2:**
```
Input: [[0,0,0],[1,1,0],[1,1,0]]

Output: 4
```
 
**Note:**

* 1 <= grid.length == grid[0].length <= 100
* grid[r][c] is 0 or 1

## Solutions

### Solution 1

* Python
```
class Solution:
    
    IJ = [(-1, -1), (0, -1), (-1, 0), (-1, 1), (0, 1), (1, 1), (1, 0), (1, -1)]
    
    def shortestPathBinaryMatrix(self, grid: List[List[int]]) -> int:
        if grid[0][0] == 1:
            return -1
        row = len(grid)
        col = len(grid[0])
        q = queue.Queue()
        q.put((0, 0))
        result = 0
        
        while not q.empty():
            size = q.qsize()
            result += 1
            for m in range(size):
                x, y = q.get()
                if grid[x][y] == 1:
                    continue
                    
                if x == row - 1 and y == col - 1:
                    return result
                
                grid[x][y] = 1
                
                for i, j in self.IJ:
                    a, b = x + i, y + j
                    if 0 <= a < row and 0 <= b < col and grid[a][b] == 0:
                        q.put((a, b))
                        
        return -1
```

Using BFS, check the shortest path layer by layer.

**Complexity:**

* **worst-case time complexity:** `O(M * N)`, where `M` is the row of the `grid`, `N` is the column of the `grid`.
* **worst-case space complexity:** `O(M * N)`, where `M` is the row of the `grid`, `N` is the column of the `grid`.

