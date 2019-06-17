# LC139. Word Break

### LeetCode

## Question

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words. You may assume the dictionary does not contain duplicate words.

**For example**
```
given
s = "leetcode",
dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".
```

## Solutions

### Solution 1

* C++
```
bool wordBreak(string s, vector<string>& wordDict) {
    int n=s.length();
    vector<bool> dp(n+1);
    dp[0] = true;
    for(int i=1; i<=n; ++i)
        for(int j=i-1; j>=0; --j)
            if(dp[j]==true)
            {
                string sub = s.substr(j, i-j);
                if(find(wordDict.begin(), wordDict.end(), sub) != wordDict.end())
                {
                    dp[i] = true;
                    break;
                }
            }
    return dp[n];
}
```

* C++
```
bool wordBreak(string s, vector<string>& wordDict) {
    int n=s.length();
    vector<bool> dp(n+1);
    dp[0] = true;
    unordered_map<string, bool>map;
    for(string word : wordDict)
        map[word] = true;
    for(int i=1; i<=n; ++i)
        for(int j=i-1; j>=0; --j)
            if(dp[j]==true)
            {
                string sub = s.substr(j, i-j);
                if(map[sub] == true)
                {
                    dp[i] = true;
                    break;
                }
            }
    return dp[n];
}
```

Using `dp[j]` to represent if you can break the string `s` at the index `j`, and the substring before `j` is breakable.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.