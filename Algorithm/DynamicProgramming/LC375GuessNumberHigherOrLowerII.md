# LC375. Guess Number Higher or Lower II

### LeetCode

## Question

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.
Every time you guess wrong, I'll tell you whether the number I picked is higher or lower.

However, when you guess a particular number x, and you guess wrong, you pay `$x`. You win the game when you guess the number I picked.

**Example:**

```
n = 10, I pick 8.

First round:  You guess 5, I tell you that it's higher. You pay $5.
Second round: You guess 7, I tell you that it's higher. You pay $7.
Third round:  You guess 9, I tell you that it's lower. You pay $9.

Game over. 8 is the number I picked.

You end up paying $5 + $7 + $9 = $21.
```

Given a particular n ≥ 1, find out how much money `at least` you need to have to guarantee a win.

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    int MinToWin(vector<vector<int>>& dp, int start, int end)
    {
        if(start >= end) return 0;
        if(dp[start][end]!=0) return dp[start][end];
        int minV = INT_MAX;
        for(int i=start; i<end; ++i)
        {
            int maxLoc = i + max(MinToWin(dp, start, i-1), MinToWin(dp, i+1,end));
            minV = min(minV, maxLoc);
        }
        dp[start][end]= minV;
        return dp[start][end];
    }
    int getMoneyAmount(int n) {
        vector<vector<int>> dp(n+1, vector<int>(n+1));
        return MinToWin(dp, 1, n);
    }
};
```

Using `dp[i][j]` to store the money `at least` you need to have to guarantee a win from number `i` to `j`.

`i + max(MinToWin(dp, start, i-1), MinToWin(dp, i+1,end));` means if you guess `i`, the maximum you need to pay.

So, always guess the `i` which you pay less than you guess other number.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>).
* **worst-case space complexity:** O(n<sup>2</sup>).