# LC474. Ones and Zeroes

### LeetCode

## Question

In the computer world, use restricted resource you have to generate maximum benefit is what we always want to pursue.

For now, suppose you are a dominator of m `0s` and n `1s` respectively. On the other hand, there is an array with strings consisting of only `0s` and `1s`.

Now your task is to find the maximum number of strings that you can form with given m `0s` and n `1s`. Each 0 and 1 can be used at most once.

**Note:**

1.	The given numbers of 0s and 1s will both not exceed 100
2.	The size of given string array won't exceed 600.

**Example 1:**
```
Input: Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3
Output: 4

Explanation: This are totally 4 strings can be formed by the using of 5 0s and 3 1s, which are “10,”0001”,”1”,”0”
```

**Example 2:**

```
Input: Array = {"10", "0", "1"}, m = 1, n = 1
Output: 2

Explanation: You could form "10", but then you'd have nothing left. Better form "0" and "1".
```

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    struct Str01{
      int zero;
      int one;
      Str01(int a, int b) : zero(a), one(b) {}
    };
    Str01 count01(string str)
    {
        int a=0, b=0;
        for(char c : str)
        {
            if(c=='0') a++;
            else b++;
        }
        return Str01(a, b);
    }
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> dp(m+1, vector<int>(n+1));
        for(string str : strs)
        {
            Str01 str01 = count01(str);
            for(int i=m; i>=str01.zero; --i)
            {
                for(int j=n; j>=str01.one; --j)
                    dp[i][j] = max(dp[i][j], 1+dp[i-str01.zero][j-str01.one]);
            }
        }
        return dp[m][n];
    }
};
```

1. Count the number of `0` and `1` of each string in `strs`.
2. Using `dp[i][j]` to store the maximum number of strings that you can form with given i 0s and j 1s.
3. `1+dp[i-str01.zero][j-str01.one]` means the maximum number of strings if count the `str01` in. 

**Complexity:**

* **worst-case time complexity:** `O(len * m * n)`, where `len` is the length of the input `strs`.
* **worst-case space complexity:** `O(m * n)`.
