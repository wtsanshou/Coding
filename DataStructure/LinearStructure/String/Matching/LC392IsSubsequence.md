# LC392. Is Subsequence

### LeetCode

## Question

Given a string s and a string t, check if s is subsequence of t.

You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100).

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).

Example 1:


s = "abc", t = "ahbgdc"
Return true.


Example 2:


s = "axc", t = "ahbgdc"
Return false.


Follow up:

If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its subsequence. In this scenario, how would you change your code?

## Solutions

### Solution 1

* C++ (69ms) 
```
bool isSubsequence(string s, string t) {
    for(int i=0, j=0; i<s.length(); ++i,++j)
    {
        while(j<t.length() && t[j] != s[i]) j++;
        if(j>=t.length()) return false;
    }
    return true;
}
```

Check each letter in `s`. Using pointer `j` to point the matched letter in `t`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `t`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* C++
```
bool isSubsequence(string s, string t) {
    int sLen = s.length(), i = 0;
    if(sLen == 0) return true;
    for(char tc : t)
        if(tc == s[i] && ++i==sLen)
            return true;
    return false;
}
```

Check each letter in `t`. Using pointer `i` to point the matched letter in `s`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `t`.
* **worst-case space complexity:** `O(1)`.

### Solution 3

* C++
```
bool isSubsequence(string s, string t) {
    int sLen = s.length(), tLen = t.length();
    if(sLen == 0) return true;
    int ss=0, se=sLen-1;
    for(int ts=0, te=tLen-1; ts<te; ++ts, --te)
        if(s[ss] == t[ts] && ++ss>se || s[se]==t[te] && --se<ss)
            return true;
    return false;
}
```

Check each letter from both left and right sides in `t`. Using pointers `ss` and `se` to point the matched letter in `s`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `t`.
* **worst-case space complexity:** `O(1)`.