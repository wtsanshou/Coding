# LC73. Set Matrix Zeroes 

### LeetCode

## Question

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.

**Follow up:**

* Did you use extra space?
* A straight forward solution using O(mn) space is probably a bad idea.
* A simple improvement uses O(m + n) space, but still not the best solution.
* Could you devise a constant space solution?

## Solutions

### Solution 1
* C++
```
void setZeroes(vector<vector<int>>& matrix) {
    int h = matrix.size();
    int w = (h>0) ? matrix[0].size() : 0;
    vector<bool> row(h);
    vector<bool> col(w);
    for(int i=0; i<h; ++i)
        for(int j=0; j<w; ++j)
            if(matrix[i][j] == 0)
                row[i]=col[j]=true;
    for(int i=0; i<h; ++i)
        for(int j=0; j<w; ++j)
            if(row[i] || col[j])
                matrix[i][j] = 0;
}
```

Using two array to memory if `ith` row and `jth` column need to set to `0`. Then based on the memory, set `0` in the `matrix`.

* **worst-case time complexity:** `O(h * w)`, where `h` is the height of the `Matrix`, `w` is the width of the `matrix`.
* **worst-case space complexity:** `O(h + w)`, where `h` is the height of the `Matrix`, `w` is the width of the `matrix`.

### Solution 2

* Java
```
public void setZeroes(int[][] matrix) {
    int h = matrix.length;
    int w = h>0 ? matrix[0].length : 0;
    boolean isColumZero = false;
    for(int i=0; i<h; i++){
        if(matrix[i][0] == 0) isColumZero = true;
        for(int j=1; j<w; j++)
            if(matrix[i][j] == 0)
                matrix[i][0] = matrix[0][j] = 0;                
    }
    for(int i=h-1; i>0; i--)
        for(int j=w-1; j>0; j--)
            if(matrix[i][0] == 0  || matrix[0][j] == 0)
                matrix[i][j] = 0;
    if(matrix[0][0] == 0)
        for(int j=1; j<w; j++)
            matrix[0][j] = 0;
    if(isColumZero)
        for(int i=0; i<h; i++)
            matrix[i][0] = 0;
}
```

Using the first row and the first colum to replace the two array to memory the `ith` row and `jth` column need to set to `0`. 

**Note:** Before lost the memory the `0` in the first colum, we have to use a boolean to memory if the first colum has `0`.

Then set `0` to the matrix except the first row and the first colum.

For the first row, we have the `0` memory in the `matrix[0][0]`.

for the first colum, we have the `0` memory in the bollean `isColumZero`.

* **worst-case time complexity:** `O(h * w)`, where `h` is the height of the `Matrix`, `w` is the width of the `matrix`.
* **worst-case space complexity:** `O(1)`
 