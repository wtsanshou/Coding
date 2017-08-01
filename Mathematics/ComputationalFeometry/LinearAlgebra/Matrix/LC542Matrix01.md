# LC542. 01 Matrix

### LeetCode

## Question

Given a matrix consists of 0 and 1, find the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

**Example 1:** 

**Input:**
```
0 0 0
0 1 0
0 0 0
```

**Output:**
```
0 0 0
0 1 0
0 0 0
```

**Example 2:**

**Input:**
```
0 0 0
0 1 0
1 1 1
```

**Output:**
```
0 0 0
0 1 0
1 2 1
```

**Note:**

1. The number of elements of the given matrix will not exceed 10,000.
2. There are at least one 0 in the given matrix.
3. The cells are adjacent in only four directions: up, down, left and right.

## Solutions

* C++1 (316ms)
```
class Solution {
public:
    void updateFromTo(int h, int w, vector<vector<int>>& matrix, vector<vector<int>>& res, bool frontToEnd)
    {
        for(int i = (frontToEnd) ? 0 : h-1; (frontToEnd) ? i<h : i>=0; (frontToEnd) ? ++i : --i)
            for(int j = (frontToEnd) ? 0 : w-1; (frontToEnd) ? j<w : j>=0; (frontToEnd) ? ++j : --j)
            {
                if(matrix[i][j] == 0) res[i][j] = 0;
                else
                {
                    if(i>0) res[i][j] = min(res[i][j], res[i-1][j]+1);
                    if(j>0) res[i][j] = min(res[i][j], res[i][j-1]+1);
                    if(i+1<h) res[i][j] = min(res[i][j], res[i+1][j]+1);
                    if(j+1<w) res[i][j] = min(res[i][j], res[i][j+1]+1);
                }
            }
    }

    vector<vector<int>> updateMatrix(vector<vector<int>>& matrix) {
        int h = matrix.size(), w=matrix[0].size();
        vector<vector<int>> res(h, vector<int>(w, 10000));
        updateFromTo(h,w,matrix,res, true);
        updateFromTo(h,w,matrix,res, false);
        return res;
    }
};
```

## Explanation

The idea is to check every element from top left to bottom right and do it again from bottom right to top left.

Each time, check four elements around to see if there is a smller distance.

* **worst-case time complexity:** O(w*h)
* **worst-case space complexity:** O(w*h)