# LC661. Image Smoother

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.

**Example 1:**

**Input:**

```
[[1,1,1],
 [1,0,1],
 [1,1,1]]
```

**Output:**

```
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
```

**Explanation:**

* For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
* For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
* For the point (1,1): floor(8/9) = floor(0.88888889) = 0

**Note:**

* The value in the given matrix is in the range of [0, 255].
* The length and width of the given matrix are in the range of [1, 150].

## Solutions

* Java1

```
class Solution {
    public int[][] imageSmoother(int[][] M) {
        int h=M.length, w=M[0].length;
        for(int i=0; i<h; ++i){
            for(int j=0; j<w; ++j){
                int ave = getAve(M, i, j);
                M[i][j] += ave<<8;
            }
        }
        
        for(int i=0; i<h; ++i){
            for(int j=0; j<w; ++j){
                M[i][j] >>= 8;
            }
        }
        return M;
    }
    
    private int getAve(int[][] M, int x, int y){
        int div=0, sum=0;
        for(int i=-1; i<=1; ++i){
            for(int j=-1; j<=1; ++j){
                if(x+i>=0 && x+i<M.length && y+j>=0 && y+j<M[0].length){
                    sum += M[x+i][y+j] & 255;
                    div++;
                }
            }
        }
        return sum/div;
    }
}
```

## Explanation

Because `The value in the given matrix is in the range of [0, 255]`, the average result will not exceed 255 (8 bits). 

Therefore, we can calculate the the average gray scale of each cell, and save the average vale into the cell number's from 9 to 16 bits. In this way the average value result will not affect the original gray scale. The same idea with <a href="../../NumberTheory/Bit/LC289GameOfLife.md">LC289. Game of Life</a>

* **worst-case time complexity:** O(h * w)
* **worst-case space complexity:** O(1)