# LC54. Spiral Matrix

### LeetCode

## Question

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

**For example,**

Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

You should return [1,2,3,6,9,8,7,4,5].

## Solutions

* C++1
```
vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int h=matrix.size();
        int w = h>0 ? matrix[0].size() : 0;
        int size = h*w;
        vector<int> res(size);
        if(size==0) return res;
        vector<vector<bool>> vis(h, vector<bool>(w));
        vis[0][0]=true;
        res[0]=matrix[0][0];
        int n=0,i=0,j=0;
        while(n<size-1)
        {
            while(j+1<w && !vis[i][j+1]) { vis[i][j+1]=true; res[++n]=matrix[i][++j];}
            while(i+1<h && !vis[i+1][j]) { vis[i+1][j]=true; res[++n]=matrix[++i][j];}
            while(j-1>=0 && !vis[i][j-1]) { vis[i][j-1]=true; res[++n]=matrix[i][--j];}
            while(i-1>=0 && !vis[i-1][j]) { vis[i-1][j]=true; res[++n]=matrix[--i][j];}
        }
        return res;
}
```

* C++2
```
vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.empty()) return vector<int>();
        vector<int> res(1, matrix[0][0]);
        int m = matrix.size(), n = matrix[0].size();
        vector<vector<bool>> visited(m, vector<bool>(n, false));
        visited[0][0]=true;
        int i=0, j=0, loop = (min(m,n)+1)/2;
        for(int k=0; k<loop; ++k)
        {
            while(j+1<n && !visited[i][j+1])
            {
                visited[i][j+1]=true;
                res.push_back(matrix[i][++j]);
            }
            while(i+1<m && !visited[i+1][j])
            {
                visited[i+1][j]= true;
                res.push_back(matrix[++i][j]);
            }
            while(j-1>=0 && !visited[i][j-1])
            {
                visited[i][j-1]=true;
                res.push_back(matrix[i][--j]);
            }
            while(i-1>=0 && !visited[i-1][j])
            {
                visited[i-1][j]=true;
                res.push_back(matrix[--i][j]);
            }
        }
        return res;
}
```

* C++3
```
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    if(matrix.empty()) return vector<int>();
    
    int m = matrix.size(), n = matrix[0].size();
    vector<int> res(m*n);
    int left=0, right=n-1, up=0, down=m-1, i=0;
    while(true)
    {
        for(int col=left; col<=right; ++col) res[i++] = matrix[up][col];
        if(++up>down) break;
        
        for(int row=up; row<=down; ++row) res[i++] = matrix[row][right];
        if(--right<left) break;
        
        for(int col=right; col>=left; --col) res[i++] = matrix[down][col];
        if(--down<up) break;
        
        for(int row=down; row>=up; --row) res[i++] = matrix[row][left];
        if(++left>right) break;
    }
    return res;
}
```

## Explanation

Loop from left to right, top to bottom, right to left, bottom to top.

Use a memory matrix to mark the recorded elements.

**Note:** The first element and the last element.

* **worst-case time complexity:** O(h * w)
* **worst-case space complexity:** O(h * w)