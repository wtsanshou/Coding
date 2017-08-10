# LC48. Rotate Image

###LeetCode

## Question

You are given an n x n 2D matrix representing an image.
Rotate the image by 90 degrees (clockwise).

Follow up:

Could you do this in-place?

## Solutions

* C++1 (6ms)
```
void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size()-1;
        for(int i=0; i<n; ++i)
        {
            for(int j=i; j<n-i; ++j)
            {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[n-j][i];
                matrix[n-j][i] = matrix[n-i][n-j];
                matrix[n-i][n-j] = matrix[j][n-i];
                matrix[j][n-i] = temp;
            }
        }
}
```

* C++2 (4ms)
```void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size()-1;
        for(int i=0; i<(n+1)/2; ++i)
        {
            for(int j=i; j<n-i; ++j)
            {
                swap(matrix[j][i], matrix[i][n-j]);
                swap(matrix[n-i][j], matrix[j][i]);
                swap(matrix[n-j][n-i], matrix[n-i][j]);
            }
        }
}
```

* Java1 (1ms)
```
public class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length-1;
        for(int i=0; i<(n+1)/2; ++i)
        {
            for(int j=i; j<n-i; ++j)
            {
                //up to left
                mySwap(matrix, i,n-j, j,i);
                //left to down
                mySwap(matrix, j,i, n-i,j);
                //down to right
                mySwap(matrix, n-i,j, n-j,n-i);
            }
        }
    }
    
    private void mySwap(int[][] matrix, int ai, int aj, int bi, int bj)
    {
        int temp = matrix[ai][aj];
        matrix[ai][aj] = matrix[bi][bj];
        matrix[bi][bj] = temp;
    }
}
```

## Explanation

* **Solution1:** keep the value `a` of position1, move the rest corresponding values of three positions one step (b->a, c->b, d->c), put the `a` in the position4.
* **Solution2:** swap `a` three time, swap `b`, `c`, `d` one time respectively. (a<->b, a<->c, a<->d).


* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)

