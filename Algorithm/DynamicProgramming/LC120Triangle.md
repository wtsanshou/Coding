# LC120. Triangle

### LeetCode

## Question

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

**Note:**

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

## Solutions

* C++1
```
int minimumTotal(vector<vector<int>>& triangle) {
    int h = triangle.size();
    for(int i=h-2; i>=0; --i)
        for(int j=0; j<triangle[i].size(); ++j)
            triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1]);
    return triangle[0][0];
}
```

* C++2
```
int minimumTotal(vector<vector<int>>& triangle) {
    vector<int> minT = triangle.back();
    for(int i=triangle.size()-2; i>=0; --i)
    {
        for(int j=0; j<triangle[i].size(); ++j)
        {
            minT[j] = triangle[i][j] + min(minT[j], minT[j+1]);
        }
    }
    return minT[0];
}
```

## Explanation

Starting from the penultimate layer to the top layer, calculate the current layer's minimum sum based on the lower layer. 

* **worst-case time complexity:** O(N<sup>2</sup>), , where `N` is the length of the input `triangle`.
* **worst-case space complexity:** O(1).