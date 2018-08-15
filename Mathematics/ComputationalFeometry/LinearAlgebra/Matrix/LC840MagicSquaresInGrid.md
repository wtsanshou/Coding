# LC840. Magic Squares In Grid

### LeetCode

## Question

A 3 x 3 magic square is a 3 x 3 grid filled with distinct numbers from 1 to 9 such that each row, column, and both diagonals all have the same sum.

Given an grid of integers, how many 3 x 3 "magic square" subgrids are there?  (Each subgrid is contiguous).

**Example 1:**
```
Input: [[4,3,8,4],
        [9,5,1,9],
        [2,7,6,2]]
Output: 1
```

**Explanation: **

The following subgrid is a 3 x 3 magic square:
```
438
951
276
```
while this one is not:
```
384
519
762
```
In total, there is only one magic square inside the given grid.

**Note:**

* 1 <= grid.length <= 10
* 1 <= grid[0].length <= 10
* 0 <= grid[i][j] <= 15

## Solutions

* Scala1
```
object Solution {
    
    val square = List(0, 1, 2)
    
    def numMagicSquaresInside(grid: Array[Array[Int]]): Int = {
        var result = 0
        var i=0
        var j=0
        for( i <- 0 to (grid.length-3); j <- 0 to (grid(0).length - 3)
           if inRange1to9(grid, i, j)){
            if(isMagicSquares(grid, i, j)) result += 1
        }
        result
    }
    
    def inRange1to9(grid: Array[Array[Int]], x: Int, y: Int): Boolean = {
        for(i <- square;j <- square){
            val element = grid(x+i){y+j}
            if(element == 0 || element > 9) return false
        }
        true
    }
    
    def isMagicSquares(grid: Array[Array[Int]], x: Int, y: Int): Boolean = {
        val sum = square.map(s => grid(x+s)(y+s)).sum
        val diagonal = square.map(s => grid(x+s)(y+2-s)).sum
        val rc = square.filter(i => {
            square.map(j => grid(x+i)(y+j)).sum != sum ||
            square.map(j => grid(x+j)(y+i)).sum != sum
        })
        
        sum == diagonal && rc.isEmpty
    }
    
}
```

## Explanation

Check each `3 x 3` subgrids.

* **worst-case time complexity:** O(w*h), where `w` is the width of the grid, `h` is the height of the grid.
* **worst-case space complexity:** O(w*h), where `w` is the width of the grid, `h` is the height of the grid.
