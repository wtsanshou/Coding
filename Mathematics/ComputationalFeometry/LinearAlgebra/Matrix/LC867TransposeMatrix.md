# LC867. Transpose Matrix

### LeetCode

## Question

Given a matrix A, return the transpose of A.

The transpose of a matrix is the matrix flipped over it's main diagonal, switching the row and column indices of the matrix.

**Example 1:**
```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: [[1,4,7],[2,5,8],[3,6,9]]
```

**Example 2:**
```
Input: [[1,2,3],[4,5,6]]
Output: [[1,4],[2,5],[3,6]]
```

**Note:**

* 1 <= A.length <= 1000
* 1 <= A[0].length <= 1000

## Solutions

* Java1
```
public int[][] transpose(int[][] A) {
    int resW = A.length;
    int resH = A[0].length;
    int[][] res = new int[resH][];
    for(int i=0; i<resH; ++i){
        res[i] = new int[resW];
        for(int j=0; j<resW; ++j){
            res[i][j] = A[j][i];
        }
    }
    return res;
}
```

## Explanation

* **worst-case time complexity:** O(h * w)
* **worst-case space complexity:** O(h * w)

