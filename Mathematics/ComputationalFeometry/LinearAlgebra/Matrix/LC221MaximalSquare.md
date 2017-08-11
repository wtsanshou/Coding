# LC221. Maximal Square

### LeetCode

## Question

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

For example, given the following matrix:

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Return 4.

## Solutions

* C++1
```
int maximalSquare(vector<vector<char>>& matrix) {
    int h = matrix.size();
    int w = h>0 ? matrix[0].size() : 0;
    vector<int> dp(w+1);
    int edge=0, topLeft=0;
    for(int i=0; i<h; ++i)
    {
        for(int j=1; j<=w; ++j)
        {
            int temp = dp[j];
            if(matrix[i][j-1]=='1')
            {
                dp[j] = min(dp[j], min(dp[j-1], topLeft)) + 1;
                edge = max(edge, dp[j]);
            }
            else
                dp[j] = 0;
            topLeft = temp;
        }
    }
    return edge*edge;
}
```

## Explanation

This is a typical dynamic programming solution. 

The idea is to check topleft 'a', up 'b' and left 'c' elements, 

1. 'a', 'b', or 'c' is/are **0**: the maximum edge is 1 for current element.
2. 'a', 'b', or 'c' are all **1**: the maximum edge for current element is 1 + minimum(edge(a), edge(b), edge(c)).

* **worst-case time complexity:** O(h*w)
* **worst-case space complexity:** O(w)

