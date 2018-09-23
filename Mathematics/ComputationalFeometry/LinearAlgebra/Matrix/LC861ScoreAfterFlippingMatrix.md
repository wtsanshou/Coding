# LC861. Score After Flipping Matrix

### LeetCode

## Question

We have a two dimensional matrix A where each value is 0 or 1.

A move consists of choosing any row or column, and toggling each value in that row or column: changing all 0s to 1s, and all 1s to 0s.

After making any number of moves, every row of this matrix is interpreted as a binary number, and the score of the matrix is the sum of these numbers.

Return the highest possible score.

**Example 1:**
```
Input: [[0,0,1,1],[1,0,1,0],[1,1,0,0]]
Output: 39
Explanation:
Toggled to [[1,1,1,1],[1,0,0,1],[1,1,1,1]].
0b1111 + 0b1001 + 0b1111 = 15 + 9 + 15 = 39
``` 

**Note:**

* 1 <= A.length <= 20
* 1 <= A[0].length <= 20
* A[i][j] is 0 or 1.

## Solutions

* Scala1
```
def matrixScore(A: Array[Array[Int]]): Int = {
    for(i <- 0 until A.length){
        if(A(i)(0) == 0){
            for(j <- 0 until A(0).length)
                A(i)(j) = A(i)(j) ^ 1
        }
    }
    for(j <- 0 until A(0).length){
        val col = for(i <- 0 until A.length) yield A(i)(j)
        if(col.sum <= A.length/2){
            for(i <- 0 until A.length)
                A(i)(j) = A(i)(j) ^ 1
        }
    }
    A.map(row => row.reverse.zipWithIndex.map(i => i._1 * Math.pow(2, i._2).toInt).sum).sum
}
```

* Scala2
```
def matrixScore(A: Array[Array[Int]]): Int = {
    val maxRow = A.map(row => if(row(0)==0) row.map(_^1) else row)
    val maxCol = maxRow.transpose.map(col => if(col.sum <= col.size/2) col.map(_^1) else col)
    maxCol.transpose.map(row => row.reduceLeft(_ * 2 + _)).sum
}
```

## Explanation

1. make sure the left first bit is `1`.
2. count `1` in each collum, make sure the sum of the `1` is more than the half size of the column in each column.

* **worst-case time complexity:** O(H * W), where `H` is the height of the input Array `A`, `W` is the width of the Array `A`.
* **worst-case space complexity:** O(H * W), where `H` is the height of the input Array `A`, `W` is the width of the Array `A`.
