# LC463. Island Perimeter

### LeetCode

## Question

You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water. Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells). The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

**Example:**
```
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]
```

**Answer:** 16

**Explanation:** The perimeter is the 16 yellow stripes in the image below:

![Island](Images/LC463IslandPerimeter.png)

## Solutions

* C++1
```
int islandPerimeter(vector<vector<int>>& grid) {
        int row = grid.size();
        int col = (row > 0) ? grid[0].size() : 0;
        int res = 0;
        for(int i=0; i<row; ++i)
        {
            for(int j=0; j<col; ++j)
            {
                if(grid[i][j] == 1)
                {
                    if(i==0 || grid[i-1][j]==0 ) res++;
                    if(j==0 || grid[i][j-1]==0) res++;
                    if(i+1==row || grid[i+1][j]==0) res++;
                    if(j+1==col || grid[i][j+1]==0) res++;
                }
            }
        }
        return res;
}
```

* Python1
```
def islandPerimeter(self, grid):
        res=0; h=len(grid); w=len(grid[0]) if h>0 else 0
        for i in range(h):
            for j in range(w):
                if grid[i][j] == 1 : 
                    if i-1<0 or grid[i-1][j]==0:
                        res += 1
                    if j-1<0 or grid[i][j-1]==0:
                        res += 1
                    if i+1==h or grid[i+1][j]==0:
                        res += 1
                    if j+1==w or grid[i][j+1]==0:
                        res += 1
        return res
```

## Explanation

The edges will not connect to land.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)