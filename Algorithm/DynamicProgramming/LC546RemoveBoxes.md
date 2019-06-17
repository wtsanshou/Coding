# LC546. Remove Boxes

### LeetCode

## Question

Given several boxes with different colors represented by different positive numbers. 

You may experience several rounds to remove boxes until there is no box left. Each time you can choose some continuous boxes with the same color (composed of k boxes, k >= 1), remove them and get `k*k` points.

Find the maximum points you can get.

**Example 1:**

```
Input:
[1, 3, 2, 2, 2, 3, 4, 3, 1]
Output:
23
Explanation:
[1, 3, 2, 2, 2, 3, 4, 3, 1] 
----> [1, 3, 3, 4, 3, 1] (3*3=9 points) (3 `2` was removed)
----> [1, 3, 3, 3, 1] (1*1=1 points) 
----> [1, 1] (3*3=9 points) 
----> [] (2*2=4 points)
```

**Note:** The number of boxes n would not exceed 100.

## Solutions

### Solution 1

* C++ (TLE)
```
int removeBoxes(vector<int>& boxes) {
    int res = 0;
    for(int i=0; i<boxes.size()-1; ++i)
    {
        if(boxes[i]<=0) continue;
        int j=i+1, count=1, temp=boxes[i];
        boxes[i] = -i;
        while(j<boxes.size() && (boxes[j]<=0 || boxes[j]==temp))
        {
            if(boxes[j]==temp)
            {
                count++;
                boxes[j] = -i;
            }
            j++;
        }
        res = max(res, count*count + removeBoxes(boxes));
        for(int b=i; b<j; ++b)
            if(boxes[b]==-i)
                boxes[b] = temp;
    }
    return res;
}
```

Check all possible solutions to remove boxes. Mark the removed boxes as `-i` and recursive down. **Back tracking** the removed boxes back to `temp` before the next recursive.

**Complexity:**

* **worst-case time complexity:** O(n<sup>n</sup>), where `n` is the length of the `boxes`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `boxes`.

### Solution 2

* C++
```
class Solution {
public:
    int DFS(vector<int>& boxes, int dp[100][100][100], int start, int end, int len)
    {
        if(start>end) return 0;
        if(dp[start][end][len] > 0) return dp[start][end][len];
        
        while(start<end && boxes[end-1]==boxes[end])
        {
            end--;
            len++;
        }
        dp[start][end][len] = DFS(boxes, dp, start, end-1, 0) + (len+1)*(len+1); //at least = 1;
        for(int i=start; i<end; ++i)
        {
            if(boxes[i]==boxes[end])
                dp[start][end][len] = max(dp[start][end][len], DFS(boxes, dp, start, i, len+1)+DFS(boxes, dp, i+1,end-1, 0)); //i+1~end-1 has used
        }
        return dp[start][end][len];
    }
    int removeBoxes(vector<int>& boxes) {
        int n=boxes.size();
        int dp[100][100][100] = {0};
        return DFS(boxes, dp, 0, n-1, 0);
    }
};
```

`dp[start][end][len]` is to represent the maximum points you can get to remove `len` boxes from box `start` to `end`.

When `len=0`, it means start to remove boxes.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `boxes`.
* **worst-case space complexity:** `O(n<sup>3</sup>)`, where `n` is the length of the `boxes`.
