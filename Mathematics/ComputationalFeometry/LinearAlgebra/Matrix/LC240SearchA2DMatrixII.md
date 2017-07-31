# LC240. Search a 2D Matrix II

### LeetCode

## Question

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.

Integers in each column are sorted in ascending from top to bottom.

**For example,**

Consider the following matrix:
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = 5, return true.

Given target = 20, return false.

## Solutions

* C++1 (59ms)
```
bool searchMatrix(vector<vector<int>>& matrix, int target) {
    int h = matrix.size();
    int w = (h>0) ? matrix[0].size() : 0;
    int i= 0, j = w-1;
    while(i<h && j>=0)
    {
        if(target == matrix[i][j]) return true;
        else if(target > matrix[i][j]) i++;
        else j--;
    }
    return false;
}
```

## Explanation

It's similar as <a href="LC74Search2DMatrix.md">LC74. Search a 2D Matrix</a>. But it's sorted from row and column. So, it cannot use binary search.

This algorithm is searching from the last element 'temp' of the first row.

* if the target > temp, the target must be in the higher row;
* if the target < temp, the target must be in the lower column;

* **worst-case time complexity:** O(max(w, h))
* **worst-case space complexity:** O(1)