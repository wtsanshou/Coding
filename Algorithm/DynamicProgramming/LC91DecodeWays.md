# LC91. Decode Ways

### LeetCode

## Question

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given an encoded message containing digits, determine the total number of ways to decode it.

**For example**

Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).
The number of ways decoding "12" is 2.

## Solutions

### Solution 1

* C++
```
int numDecodings(string s) {
    int n = s.length();
    if(n==0) return 0;
    vector<int> dp(n+1);
    dp[n] = 1;
    dp[n-1] = s[n-1]=='0' ? 0 : 1;
    for(int i=n-2; i>=0; --i)
        if(s[i] != '0')
            dp[i] = stoi(s.substr(i,2))<=26 ? dp[i+1]+dp[i+2] : dp[i+1];
    return dp[0];
}
```

Using a `n+1` length `dp` to store the number of ways decoding. `dp[i]` is to store the number of ways decoding from index `i` to the end of the string `s`.

From right to left, check two char each time, if it's less or equal than `26`, `dp[i] = dp[i+1]+dp[i+2]`.

`if(s[i] == '0')`, `dp[i]` will be `0`.

**Note** the last char in the string `s` could be `0`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.