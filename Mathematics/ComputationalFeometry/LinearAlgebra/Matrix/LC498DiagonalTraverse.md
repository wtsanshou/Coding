# LC498. Diagonal Traverse

### LeetCode

## Question

Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.

**Example:**
```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output:  [1,2,4,7,5,3,6,8,9]
```

**Explanation:**

![LC498. Diagonal Traverse](Images/LC498DiagonalTraverse.png)

**Note:**

1.	The total number of elements of the given matrix will not exceed 10,000.

## Solutions

### Solution 1

* C++ (88ms)
```
vector<int> findDiagonalOrder(vector<vector<int>>& matrix) {
    int h = matrix.size();
    int w = (h>0) ? matrix[0].size() : 0;
    vector<int> res(h*w);
    int id=0;
    for(int i=0; i<h+w-1; ++i)
    {
        int lb = max(0, i-w+1), ub = min(i, h-1);
        if(i%2 == 0)
            for(int j=ub; j>=lb; --j)
                res[id++] = matrix[j][i-j];
        else
            for(int j=lb; j<=ub; ++j)
                res[id++] = matrix[j][i-j];
    }
    return res;
}
```

It needs to travel (h+w-1) times to get the diagonal order. 

In even time, we read from left-bottom to up-right. `matrix[j][i-j]`: row down and column up.

In odd time, we read from up-right to left-bottom. `matrix[j][i-j]`: row up and column down.

* **worst-case time complexity:** `O(M*N)`, where M rows, N columns of the `matrix`.
* **worst-case space complexity:** `O(M*N)`, where M rows, N columns of the `matrix`.