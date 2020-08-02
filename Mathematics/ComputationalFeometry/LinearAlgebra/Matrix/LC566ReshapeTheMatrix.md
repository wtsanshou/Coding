# LC566. Reshape the Matrix

### LeetCode

## Question

In MATLAB, there is a very useful function called 'reshape', which can reshape a matrix into a new one with different size but keep its original data.

You're given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively.

The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the 'reshape' operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

**Example 1:**
```
Input: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
```

```
Output: 
[[1,2,3,4]]
```

**Explanation:**

The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is an 1 * 4 matrix, fill it row by row by using the previous list.

**Example 2:**
```
Input: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
```

```
Output: 
[[1,2],
 [3,4]]
```

**Explanation:**

There is no way to reshape a 2 * 2 matrix to a 2 * 4 matrix. So output the original matrix.

**Note:**

1. The height and width of the given matrix is in range [1, 100].
2. The given r and c are all positive.

## Solutions

* C++1
```
vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
    int h=nums.size(), w=nums[0].size();
    if(r*c != h*w) return nums;
    vector<vector<int>> res(r, vector<int>(c));
    for(int i=0, k=0; i<r; ++i)
        for(int j=0; j<c; ++j, ++k)
            res[i][j] = nums[k/w][k%w];
    return res;
}
```

* Python
```
def matrixReshape(self, nums: List[List[int]], r: int, c: int) -> List[List[int]]:
    row = len(nums)
    col = len(nums[0]) if row > 0 else 0
    if row * col != r * c:
        return nums
    
    one = []
    for line in nums:
        one += line
        
    result = []
    for i in range(int(len(one) / c)):
        result.append(one[i * c:i * c + c])
    
    return result
```

## Explanation

- **worst-case time complexity:** O(h * w)
- **worst-case space complexity:** O(h * w)