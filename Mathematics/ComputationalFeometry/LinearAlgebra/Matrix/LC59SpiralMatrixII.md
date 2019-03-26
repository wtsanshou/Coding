# LC59. Spiral Matrix II

### LeetCode

## Question

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

**For example**
```
Given n = 3,
You should return the following matrix:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

## Solutions

### Solution 1

* C++ (3ms)
```
vector<vector<int>> generateMatrix(int n) {
    vector<vector<int>> res(n, vector<int>(n));
    int val=0, i=0, j=-1;
    while(val<n*n)
    {
        while(j+1<n && res[i][j+1]==0) res[i][++j] = ++val;
        while(i+1<n && res[i+1][j]==0) res[++i][j] = ++val;
        while(j-1>=0 && res[i][j-1]==0) res[i][--j] = ++val;
        while(i-1>=0 && res[i-1][j]==0) res[--i][j] = ++val;
    }
    return res;
}
```

Travel the matrix with spiral order and fill in numbers. Just be careful the boundaries: at the beginning, the boundaries are the border of the matrix; after spiral insid of the matrix, the boundaries are the locations where already have numbers filled in.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the input value `n`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the input value `n`.
