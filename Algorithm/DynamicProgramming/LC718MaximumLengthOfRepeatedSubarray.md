# LC718. Maximum Length of Repeated Subarray

### LeetCode

## Question

Given two integer arrays `A` and `B`, return the maximum length of an subarray that appears in both arrays.

**Example 1:**
```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

**Note:**

* 1 <= len(A), len(B) <= 1000
* 0 <= A[i], B[i] < 100

## Solutions

### Solution 1

* Java
```
public int findLength(int[] A, int[] B) {
    int n1 = A.length;
    int n2 = B.length;
    int max = 0;
    int[][] dp = new int[n1 + 1][n2 + 1];
    
    for (int i = 1; i <= n1; i++) {
        for (int j = 1; j <= n2; j++) {
            if (A[i - 1] == B[j - 1])
                dp[i][j] = dp[i - 1][j - 1] + 1;
            else
                dp[i][j] = 0;
            max = Math.max(max, dp[i][j]);
        }
    }
    
    return max;
}
```

### Solution 2

* Java (Roll Optimize)
```
public int findLength(int[] A, int[] B) {
    int n1 = A.length;
    int n2 = B.length;
    int max = 0;
    int[][] dp = new int[2][n2 + 1];
    
    for (int i = 1; i <= n1; i++) {
        for (int j = 1; j <= n2; j++) {
            if (A[i - 1] == B[j - 1])
                dp[i % 2][j] = dp[(i - 1) % 2][j - 1] + 1;
            else
                dp[i % 2][j] = 0;
            max = Math.max(max, dp[i % 2][j]);
        }
    }
    
    return max;
}
```

* Java1
```
public int findLength(int[] A, int[] B) {
    if(A.length < B.length) return findLength(B, A);
    int n = B.length, result=0;
    int[] dp = new int[n];
    for(int a : A){
        int upperLine=0;
        for(int i=0; i<n; ++i){
            int temp = upperLine;
            upperLine = dp[i];
            dp[i] = a == B[i] ? temp + 1 : 0;
            
            result = Math.max(result, dp[i]);
        }
    }
    return result;
}
```

## Explanation

It's similar as a classic dynamic programming algorithm `Longest common substring` I have learned in Southeast University. The question  needs to return the `Longest common substring`. So, it uses a 2D array to remember the paths of all common substring.

Here, we don't need to return the longest repeated subarry. So, 1D array is enough.

```
    B   2   1   2   3   4
A
1       0   1   0   0   0
2       1   0   2   0   0
3       0   0   0   3   0
.
.
.
```

If found a common elements, set current `dp` as `top left dp` + `1`,

else, set current `dp` as `0`

* **worst-case time complexity:** O(M*N), , where `M` is the length of the input `A`, `N` is the length of the input `B`.
* **worst-case space complexity:** O(min(M, N)), where `M` is the length of the input `A`, `N` is the length of the input `B`.