# LC467. Unique Substrings in Wraparound String

### LeetCode

## Question

Consider the string s to be the infinite wraparound string of "abcdefghijklmnopqrstuvwxyz", so s will look like this: "...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd....".

Now we have another string p. Your job is to find out how many unique non-empty substrings of p are present in s. In particular, your input is the string p and you need to output the number of different non-empty substrings of p in the string s.

**Note:** p consists of only lowercase English letters and the size of p might be over 10000.

**Example 1:**

```
Input: "a"
Output: 1

Explanation: Only the substring "a" of string "a" is in the string s.
```

**Example 2:**

```
Input: "cac"
Output: 2

Explanation: There are two substrings "a", "c" of string "cac" in the string s.
```

**Example 3:**

```
Input: "zab"
Output: 6

Explanation: There are six substrings "z", "a", "b", "za", "ab", "zab" of string "zab" in the string s.
```

## Solutions

### Solution 1

* C++
```
int findSubstringInWraproundString(string p) {
    if(p.empty()) return 0;
    vector<int> dp(26);
    dp[p[0]-'a'] = 1;
    for(int i=1, curMax=1, gap = 'a'-'z'; i<p.length(); ++i)
    {
        curMax = (i!=0 && (p[i]-p[i-1]==1 || p[i]-p[i-1]==gap)) ? curMax+1 : 1;
        dp[p[i]-'a'] = max(dp[p[i]-'a'], curMax);
    }
    return accumulate(dp.begin(), dp.end(), 0);
}
```

Using `dp[i]` to represent the maximum number of unique non-empty substrings which is starting from the letter `'a'+i`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `p`.
* **worst-case space complexity:** `O(26)`.