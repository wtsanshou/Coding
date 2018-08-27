# LC892. Surface Area of 3D Shapes

### LeetCode

## Question

On a N * N grid, we place some 1 * 1 * 1 cubes.

Each value v = grid[i][j] represents a tower of v cubes placed on top of grid cell (i, j).

Return the total surface area of the resulting shapes.

 

**Example 1:**
```
Input: [[2]]
Output: 10
```

**Example 2:**
```
Input: [[1,2],[3,4]]
Output: 34
```

**Example 3:**
```
Input: [[1,0],[0,2]]
Output: 16
```

**Example 4:**
```
Input: [[1,1,1],[1,0,1],[1,1,1]]
Output: 32
```

**Example 5:**
```
Input: [[2,2,2],[2,1,2],[2,2,2]]
Output: 46
```

**Note:**

* 1 <= N <= 50
* 0 <= grid[i][j] <= 50

## Solutions

* Scala1
```
object Solution {
    def surfaceArea(grid: Array[Array[Int]]): Int = {
        val res = for(i <- 0 until grid.size; j <- 0 until grid(0).size) yield getTopCover(grid, i, j)
        res.sum + grid.map(row => row.map(e => if(e>0) 1 else 0).sum).sum
    }
    
    def getTopCover(grid: Array[Array[Int]], i: Int, j: Int): Int = {
        if(grid(i)(j) == 0) return 0
        var res = 1
        if(i==0 || grid(i-1)(j) < grid(i)(j)) res += grid(i)(j) - (if(i==0) 0 else grid(i-1)(j))
        if(j==0 || grid(i)(j-1) < grid(i)(j)) res += grid(i)(j) - (if(j==0) 0 else grid(i)(j-1))
        if(i==grid.size-1 || grid(i+1)(j) < grid(i)(j)) res += grid(i)(j) - (if(i==grid.size-1) 0 else grid(i+1)(j))
        if(j==grid(0).size-1 || grid(i)(j+1) < grid(i)(j)) res += grid(i)(j) - (if(j==grid(0).size-1) 0 else grid(i)(j+1))
        res
    }
}
```

## Explanation

Check each cell in the grid, if the cell is convex, calculate the surface around the top. The top and the bottom are easy to get.

* **worst-case time complexity:** O(N<sup>2</sup>)
* **worst-case space complexity:** O(N)
