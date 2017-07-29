# LC74. Search a 2D Matrix

### LeetCode

## Question

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

* Integers in each row are sorted from left to right.
* The first integer of each row is greater than the last integer of the previous row.

For example,

Consider the following matrix:
```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```

Given target = 3, return true.

## Solutions

* C++1
```
bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int h = matrix.size();
        int w = (h>0) ? matrix[0].size() : 0;
        int i=0, j= h*w - 1;
        while(i<=j)
        {
            int mid = i + (j-i)/2;
            int ele = matrix[mid/w][mid%w];
            if(ele == target) return true;
            else if(ele > target) j = mid-1;
            else i = mid+1;
        }
        return false;
    }
```

## Explanation

It's like cutting a sorted array to a 2D array.

Like search a element in a sorted array, binary search is fastest way.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)