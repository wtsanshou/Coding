# LC552. Student Attendance Record II

### LeetCode

## Question

Given a positive integer n, return the number of all possible attendance records with length n, which will be regarded as rewardable. The answer may be very large, return it after mod 109 + 7.

A student attendance record is a string that only contains the following three characters:

1.	'A' : Absent.
2.	'L' : Late.
3.	'P' : Present.

A record is regarded as rewardable if it doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).

**Example 1:**

```
Input: n = 2
Output: 8 
Explanation:
There are 8 records with length 2 will be regarded as rewardable:
"PP" , "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" won't be regarded as rewardable owing to more than one absent times. 
```

**Note:** The value of n won't exceed 100,000.

## Solutions

### Solution 1

* C++
```
int checkRecord(int n) {
    int mod = 1000000007;
    int dp[n+1][2][3];
    for(int i=0; i<2; ++i)
        for(int j=0; j<3; ++j)
            dp[0][i][j] = 1;
    for(int p=1; p<=n; ++p)
    {
        for(int a=0; a<2; ++a)
        {
            for(int L=0; L<3; ++L)
            {
                int val = dp[p-1][a][2];
                if(a>0) val = (val + dp[p-1][a-1][2]) % mod;
                if(L>0) val = (val + dp[p-1][a][L-1]) % mod;
                dp[p][a][L] = val;
            }
        }
    }
    return dp[n][1][2];
}
```

`dp[n][i][j]` means `n` records contain `i` times `Absent` and `j` times `Late`.

**Complexity:**

* **worst-case time complexity:** `O(n)`.
* **worst-case space complexity:** `O(n)`.