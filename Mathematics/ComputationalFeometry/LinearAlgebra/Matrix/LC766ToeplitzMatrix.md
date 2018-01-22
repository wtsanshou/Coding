# LC766. Toeplitz Matrix

### LeetCode

## Question

A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same element.

Now given an M x N matrix, return True if and only if the matrix is Toeplitz.
 
**Example 1:**

**Input:** 

```
matrix = 
[[1,2,3,4],
 [5,1,2,3],
 [9,5,1,2]]
```

**Output:**
```
True
```

**Explanation:**
```
1234
5123
9512
```

In the above grid, the diagonals are "[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]", and in each diagonal all elements are the same, so the answer is True.

**Example 2:**

Input: 
```
matrix = 
[[1,2],
 [2,2]]
```

**Output:**
```
False
```

**Explanation:**

The diagonal "[1, 2]" has different elements.

**Note:**

* matrix will be a 2D array of integers.
* matrix will have a number of rows and columns in range [1, 20].
* matrix[i][j] will be integers in range [0, 99].

## Solutions

* Java1
```
public boolean isToeplitzMatrix(int[][] matrix) {
        int h = matrix.length;
        int w = matrix[0].length;
        int n = h+w-1;
        int[] dia = new int[n];
        for(int i=h; i>1; --i)
            dia[h-i] = matrix[i-1][0];
        for(int j=0; j<w; ++j)
            dia[h+j-1] = matrix[0][j];
        for(int i=1; i<h; ++i){
            for(int j=1; j<w; ++j){
                if(matrix[i][j] != dia[h-i+j-1])
                    return false;
            }
        }
        return true;
    }
```

## Explanation

Save the 0<sup>th</sup> column and the 0<sup>th</sup> row into an array `dia`.

Compare each element with the above array. The `matrix[0][0]` is at the `dia[h-1]`. So, each element `matrix[i][j]` match the element `dia[h-i+j-1]` in the array.

* **worst-case time complexity:** O(h * w)
* **worst-case space complexity:** O(h + w)