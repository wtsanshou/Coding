# LC712. Minimum ASCII Delete Sum for Two Strings

### LeetCode

## Question

Given two strings s1, s2, find the lowest ASCII sum of deleted characters to make two strings equal.

**Example 1:**

```
Input: s1 = "sea", s2 = "eat"
Output: 231
```

**Explanation:** 

Deleting "s" from "sea" adds the ASCII value of "s" (115) to the sum.

Deleting "t" from "eat" adds 116 to the sum.

At the end, both strings are equal, and 115 + 116 = 231 is the minimum sum possible to achieve this.

**Example 2:**

```
Input: s1 = "delete", s2 = "leet"
Output: 403
```

**Explanation:** 

Deleting "dee" from "delete" to turn the string into "let",
adds 100[d]+101[e]+101[e] to the sum.  Deleting "e" from "leet" adds 101[e] to the sum.

At the end, both strings are equal to "let", and the answer is 100+101+101+101 = 403.

If instead we turned both strings into "lee" or "eet", we would get answers of 433 or 417, which are higher.

**Note:**

* 0 < s1.length, s2.length <= 1000.
* All elements of each string will have an ASCII value in [97, 122].

## Solutions

* C#1
```
public int MinimumDeleteSum(string s1, string s2) {
    int n1=s1.Length, n2=s2.Length;
    int[,] dp = new int[n1+1,n2+1];
    for(int i=1; i<=n1; ++i)
        dp[i,0] = dp[i-1,0] + (int)s1[i-1];
    for(int j=1; j<=n2; ++j)
        dp[0,j] = dp[0,j-1] + (int)s2[j-1];
    for(int i=1; i<=n1; ++i)
        for(int j=1; j<=n2; ++j)
                dp[i,j] = (s1[i-1] == s2[j-1]) ? dp[i-1,j-1]
                                               : Math.Min(dp[i-1,j]+(int)s1[i-1], dp[i,j-1]+(int)s2[j-1]);
    return dp[n1,n2];
}
```

## Explanation

It's quite like the question "Find the longest common substring from two strings". Here consider the ASCII value.

* **worst-case time complexity:** O(m*n)
* **worst-case space complexity:** O(m*n)