# LC131. Palindrome Partitioning

### LeetCode

## Question

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

**For example**

```
given s = "aab",
Return
[
  ["aa","b"],
  ["a","a","b"]
]
```

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    bool isPalindrome(string& s, int start, int end)
    {
        while(start<end)
        {
            if(s[start++]!= s[end--])
                return false;
        }
        return true;
    }
    void PPHelper(vector<vector<string>>& res, vector<string>& arow, string& s, int start, int len)
    {
        if(start==len)
            res.push_back(arow);
        
        for(int i=start; i<len; ++i)
        {
            if(isPalindrome(s, start, i))
            {
                arow.push_back(s.substr(start, i-start+1));
                PPHelper(res, arow, s, i+1, len);
                arow.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        vector<vector<string>> res;
        int len = s.length();
        if(len<=0) return res;
        vector<string> arow;
        PPHelper(res, arow, s, 0, len);
        return res;
    }
};
```

* C++
```
class Solution {
public:
    bool isPalindrome(string& s)
    {
        int i=0, j=s.length()-1;
        while(i<j)
            if(s[i++] != s[j--]) return false;
        return true;
    }
    void dfs(vector<vector<string>>& res, vector<string>& aRow, string & s, vector<vector<int>>& visitPali, int start)
    {
        if(start >= s.length())
        {
            res.push_back(aRow);
        }
        for(int len=1; len<=s.length()-start; ++len)
        {
            string sub = s.substr(start, len);
            if(visitPali[start][start+len]==2)
            {
                aRow.push_back(sub);
                dfs(res, aRow, s, visitPali, start+len);
                aRow.pop_back();
            }
            else if(visitPali[start][start+len]==0)
            {
                if(isPalindrome(sub))
                {
                    visitPali[start][start+len] = 2;
                    aRow.push_back(sub);
                    dfs(res, aRow, s, visitPali, start+len);
                    aRow.pop_back();
                }
                else
                    visitPali[start][start+len] = 1;
            }
        }
    }
    vector<vector<string>> partition(string s) {
        vector<vector<string>> res;
        vector<string> aRow;
        vector<vector<int>> visitPali(s.length(), vector<int>(s.length()+1));
        for(int i=0;i<s.length(); ++i)
            visitPali[i][1] = 2;
        dfs(res, aRow, s, visitPali, 0);
        return res;
    }
};
```

* C++
```
class Solution {
public:
    void PPHelper(vector<vector<string>>& res, vector<string>& arow, string& s, int start, int len)
    {
        if(start==len)
        {
            res.push_back(arow);
        }
        string str = ""; //key point
        for(int i=start; i<len; ++i)
        {
            str+=s[i];
            if(str == string(str.rbegin(), str.rend()))
            {
                arow.push_back(str);
                PPHelper(res, arow, s, i+1, len);
                arow.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        vector<vector<string>> res;
        int len = s.length();
        vector<string> arow;
        PPHelper(res, arow, s, 0, len);
        return res;
    }
};
```

Normally, `Back tracking` is the method of solving this kind of seeking all possible palindrome partitioning question.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of `s`.
* **worst-case space complexity:** O(n), where `n` is the length of `s`.

## Follow up

* What if duplicated is not allowed?
