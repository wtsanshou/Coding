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