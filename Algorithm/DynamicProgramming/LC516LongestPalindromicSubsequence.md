# LC516. Longest Palindromic Subsequence

### LeetCode

## Question

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

**Example 1:**
```
Input:
"bbbab"
Output:
4
One possible longest palindromic subsequence is "bbbb".
```

**Example 2:**

```
Input:
"cbbd"
Output:
2
One possible longest palindromic subsequence is "bb".
```

## Solutions

### Solution 1

* C++ (TLE)
```
class Solution {
public:
    int RescursivePalindrome(string s, vector<vector<int>>& dp, int start, int end)
    {
        if(dp[start][end] != 0) return dp[start][end];
        if(start > end) return 0;
        if(start == end) return 1;
        dp[start][end] = (s[start] == s[end]) ? RescursivePalindrome(s, dp, start+1, end-1) + 2 
    : max(RescursivePalindrome(s, dp, start+1, end), RescursivePalindrome(s, dp, start, end-1));
        return dp[start][end];
    }
    int longestPalindromeSubseq(string s) {
        int n = s.length();
        if(n==0) return 0;
        vector<vector<int>> dp(n, vector<int>(n));
        return RescursivePalindrome(s, dp, 0, n-1);
    }
};
```

Using a 2D array to store the length of the longest palindromic subsequence from `i` to `j`.

From left and right recursive to the middle. If `s[start] == s[end]`, recursive the subsequence from `start+1` to `end-1`, else compare the subsequence from `start` to `end-1` and subsequence from `start+1` to `end`.

Finally, `dp[start][end]` is the result.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the input `s`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of the input `s`.

### Solution 2

* C++ (49ms)
```
int longestPalindromeSubseq(string s) {
    int n = s.length();
    if(n==0) return 0;
    vector<vector<int>> dp(n, vector<int>(n));
    for(int i=n-1; i>=0; --i)
    {
        dp[i][i] = 1;
        for(int j=i+1; j<n; ++j)
            dp[i][j] = (s[i]==s[j]) ? dp[i+1][j-1] + 2
                                    : max(dp[i+1][j], dp[i][j-1]);
    }
    return dp[0][n-1];
}
```

Checking from small length subsequence first, save the length of the longest palindromic subsequence from `i` to `j` to `dp[i][j]`.

Finally, `dp[0][n-1]` is the result.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `s`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the length of the input `s`.
