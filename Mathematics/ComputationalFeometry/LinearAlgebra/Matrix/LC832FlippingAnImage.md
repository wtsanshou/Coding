# LC832. Flipping an Image

### LeetCode

## Question

Given a binary matrix A, we want to flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.  For example, flipping [1, 1, 0] horizontally results in [0, 1, 1].

To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting [0, 1, 1] results in [1, 0, 0].

**Example 1:**
```
Input: [[1,1,0],[1,0,1],[0,0,0]]
Output: [[1,0,0],[0,1,0],[1,1,1]]
Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]
```

**Example 2:**
```
Input: [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
Output: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]].
Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```

**Notes:**

* 1 <= A.length = A[0].length <= 20
* 0 <= A[i][j] <= 1

## Solutions

* Java1
```
class Solution {
    public int[][] flipAndInvertImage(int[][] A) {
        int h = A.length, w = A[0].length;
        for(int i=0; i<h; ++i){
            for(int j=0; j<w/2; ++j){
                int temp = invert(A[i][j]);
                A[i][j] = invert(A[i][w-j-1]);
                A[i][w-j-1] = temp;
            }
            if(w%2 != 0) A[i][w/2] = invert(A[i][w/2]);
        }
        return A;
    }
    
    private int invert(int target){
        return target==0 ? 1 : 0;
    }
}
```

* Java (344 ms,  58.1 MB)
```
def flipAndInvertImage(A: Array[Array[Int]]): Array[Array[Int]] = {
    val flip = A.map(a => a.reverse)
    flip.map(F => F.map(f => f^1))
}
```

## Explanation

Invert both elements when fliping them. 

* **worst-case time complexity:** `O(W * H)`, `W` is the width the `grid`, `H` is the height of the `grid`.
* **worst-case space complexity:** `O(1)`.


