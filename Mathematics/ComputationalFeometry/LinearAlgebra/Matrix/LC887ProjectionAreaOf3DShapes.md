# LC887. Projection Area of 3D Shapes

### LeetCode

## Question

On a N * N grid, we place some 1 * 1 * 1 cubes that are axis-aligned with the x, y, and z axes.

Each value v = grid[i][j] represents a tower of v cubes placed on top of grid cell (i, j).

Now we view the projection of these cubes onto the xy, yz, and zx planes.

A projection is like a shadow, that maps our 3 dimensional figure to a 2 dimensional plane. 

Here, we are viewing the "shadow" when looking at the cubes from the top, the front, and the side.

Return the total area of all three projections.

**Example 1:**
```
Input: [[2]]
Output: 5
```

**Example 2:**
```
Input: [[1,2],[3,4]]
Output: 17
Explanation: 
Here are the three projections ("shadows") of the shape made with each axis-aligned plane.
```
![LC887. Projection Area of 3D Shapes](Images/LC887ProjectionAreaOf3DShapes.png)

**Example 3:**
```
Input: [[1,0],[0,2]]
Output: 8
```

**Example 4:**
```
Input: [[1,1,1],[1,0,1],[1,1,1]]
Output: 14
```

**Example 5:**
```
Input: [[2,2,2],[2,1,2],[2,2,2]]
Output: 21
```

**Note:**

* 1 <= grid.length = grid[0].length <= 50
* 0 <= grid[i][j] <= 50

## Solutions

* Scala1
```
def projectionArea(grid: Array[Array[Int]]): Int = {
    val xy = grid.flatten.filter(v => v>0).size;
    val yz = grid.map(g => g.max).sum
    val xz = grid.foldLeft(grid.head){
        (res, cur) => for(i <- res.indices){
            res.update(i,Math.max(res(i), cur(i)))
        }
        res
    }.sum
    xy + yz + xz
}
```

* Scala1
```
def projectionArea(grid: Array[Array[Int]]): Int = {
    val xy = grid.flatten.filter(v => v>0).size;
    val yz = grid.map(g => g.max).sum
    val xz = grid.foldLeft(grid.head){
        (res, cur) => res.zipWithIndex.map{
            case (r, i) => Math.max(r, cur(i))
        }
    }.sum
    xy + yz + xz
}
```

## Explanation

xy -> count number of grid with positive value;

yz -> sum the maximum value of each row

xz -> sum the maximum value of each column

* **worst-case time complexity:** O(n<sup>2</sup>), where n is length of the grid.
* **worst-case space complexity:** O(n<sup>2</sup>), where n is length of the grid.
