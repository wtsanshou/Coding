# LC583. Delete Operation for Two Strings

### LeetCode

## Question

Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, where in each step you can delete one character in either string.

Example 1:


Input: "sea", "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".


Note:

1.	The length of given words won't exceed 500.
2.	Characters in given words can only be lower-case letters.

## Solutions

### Solution 1
* C++ (TLE)
```
class Solution {
public:
    int LCS(string word1, int i1, string word2, int i2)
    {
        if(i1==0 || i2==0) return 0;
        else if(word1[i1-1]==word2[i2-1])
            return 1 + LCS(word1, i1-1, word2, i2-1);
        else
            return max(LCS(word1, i1-1, word2, i2), LCS(word1, i1, word2, i2-1));
    }
    int minDistance(string word1, string word2) {
        return word1.length()+word2.length() - 2*LCS(word1, word1.length(), word2, word2.length());
    }
};
```

The idea is to find the length of the longest common substring of `word1` and `word2`.

Each time check the last letter of the two `word1` and `word2`. 

**Complexity:**

* **worst-case time complexity:** O(2<sup>n1+n2</sup>), where `n1` is the length of `word1`, `n2` is the length of `word2`.
* **worst-case space complexity:** `O(n1 + n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.

### Solution 2

* C++ (with memory)
```
class Solution {
public:
    int LCS(string word1, int i1, string word2, int i2, vector<vector<int>>& mem)
    {
        if(i1==0 || i2==0) return 0;
        if(mem[i1][i2]>0) return mem[i1][i2];
        if(word1[i1-1]==word2[i2-1])
            mem[i1][i2] = 1 + LCS(word1, i1-1, word2, i2-1, mem);
        else
            mem[i1][i2] = max(LCS(word1, i1-1, word2, i2, mem), LCS(word1, i1, word2, i2-1, mem));
        return mem[i1][i2];
    }
    int minDistance(string word1, string word2) {
        int n1=word1.length(), n2=word2.length();
        vector<vector<int>> mem(n1+1, vector<int>(n2+1));
        return n1 + n2 - 2*LCS(word1, n1, word2, n2, mem);
    }
};
```

The idea is to find the length of the longest common substring of `word1` and `word2`. But here use `mem[i1][i2]` to store the the length of the longest common substring of `word1`'s substring `[0,i1]` and `word2`'s substring `[0,i2]`.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n1+n2</sup>), where `n1` is the length of `word1`, `n2` is the length of `word2`.
* **worst-case space complexity:** `O(n1 * n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.

### Solution 3

* C++
```
int minDistance(string word1, string word2) {
    int n1=word1.length(), n2=word2.length();
    vector<vector<int>> dp(n1+1, vector<int>(n2+1));
    for(int i1=1; i1<=n1; ++i1)
        for(int i2=1; i2<=n2; ++i2)
            if(word1[i1-1]==word2[i2-1])
                dp[i1][i2] = 1+dp[i1-1][i2-1];
            else
                dp[i1][i2] = max(dp[i1-1][i2], dp[i1][i2-1]);
    return n1 + n2 - 2*dp[n1][n2];
}
```

Instead of recursive, using iterative and DP.

`dp[i1][i2]` is to store the the length of the longest common substring of `word1`'s substring `[0,i1]` and `word2`'s substring `[0,i2]`.

**Complexity:**

* **worst-case time complexity:** `O(n1 * n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.
* **worst-case space complexity:** `O(n1 * n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.

### Solution 4
* C++
```
int minDistance(string word1, string word2) {
    int n1=word1.length(), n2=word2.length();
    vector<vector<int>> dp(n1+1, vector<int>(n2+1));
    for(int i1=0; i1<=n1; ++i1)
        for(int i2=0; i2<=n2; ++i2)
            if(i1==0 || i2==0)
                dp[i1][i2] = i1+i2;
            else if(word1[i1-1]==word2[i2-1])
                dp[i1][i2] = dp[i1-1][i2-1];
            else
                dp[i1][i2] = 1 + min(dp[i1-1][i2], dp[i1][i2-1]);
    return dp[n1][n2];
}
```

Here `dp[i1][i2]` is to directly store the minimum number of deletes for the `word1`'s substring `[0,i1]` and `word2`'s substring `[0,i2]`.

**Complexity:**

* **worst-case time complexity:** `O(n1 * n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.
* **worst-case space complexity:** `O(n1 * n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.

### Solution 5

* C++
```
int minDistance(string word1, string word2) {
    int n1=word1.length(), n2=word2.length();
    vector<int> dp(n2+1);
    for(int i1=0; i1<=n1; ++i1)
    {
        vector<int> temp = dp;
        for(int i2=0; i2<=n2; ++i2)
            if(i1==0 || i2==0)
                dp[i2] = i1+i2;
            else if(word1[i1-1]==word2[i2-1])
                dp[i2] = temp[i2-1];
            else
                dp[i2] = 1 + min(dp[i2], dp[i2-1]);
    }
    return dp[n2];
}
```

Based on the **Solution 4**, we can see only `i1-1` or `i2-1` will be checked during the DP process. So we can just use 1D array for the `dp`, just need a `temp` to remember the previous `dp`.

**Complexity:**

* **worst-case time complexity:** `O(n1 * n2)`, where `n1` is the length of `word1`, `n2` is the length of `word2`.
* **worst-case space complexity:** `O(n2)`, where `n2` is the length of `word2`.
