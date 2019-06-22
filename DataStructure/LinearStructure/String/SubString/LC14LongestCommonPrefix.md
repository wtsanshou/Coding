# LC14. Longest Common Prefix

### LeetCode

## Question

Write a function to find the longest common prefix string amongst an array of strings.

## Solutions

### Solution 1

* C++ (9ms)
```
string longestCommonPrefix(vector<string>& strs) {
    int wordsLen=strs.size();
    int firstWordLen = (wordsLen>0) ? strs[0].size() : 0;
    string res;
    for(int i=0; i<firstWordLen; ++i)
    {
        for(int j=1; j<wordsLen; ++j)
        {
            if(strs[j].size()<i+1 || strs[j][i]!=strs[0][i]) return res;
        }
        res +=strs[0][i];
    }
    return res;
}
```

* C++ (4ms) 
```
string longestCommonPrefix(vector<string>& strs) {
    string res = "";
    bool exist[128] = {0};
    for(int j = 0; strs.size()>0; j++)
    {
        exist[strs[0][j]] = true;
        for(int i=0; i<strs.size(); i++)
        {
            if(j>=strs[i].size() || !exist[strs[i][j]])
                return res;
        }
        res += strs[0][j];
        exist[strs[0][j]] = false;
    }
    return res;
}
```

* C++ (4ms) 
```
string longestCommonPrefix(vector<string>& strs) {
    string res = "";
    for(int j = 0; strs.size()>0; j++)
    {
        for(int i=0; i<strs.size(); i++)
        {
            if(j>=strs[i].size() || (i>0 && strs[i][j] != strs[i-1][j]))
                return res;
        }
        res += strs[0][j];
    }
    return res;
}
```

* Java (1ms) 
```
public String longestCommonPrefix(String[] strs) {
    if(strs.length == 0) return "";
    String res = strs[0];
    for(int i=0; i<strs.length; ++i)
    {
        while(strs[i].indexOf(res)!=0)
            res = res.substring(0, res.length()-1);
    }
    return res;
}
```

* Java (5ms) O(mn)
```
public String longestCommonPrefix(String[] strs) {
    StringBuilder res = new StringBuilder();
    for(int i=0; strs.length>0; ++i)
    {
        for(int j=0; j<strs.length; ++j)
        {
            if(i>=strs[j].length() || (j>0 &&strs[j].charAt(i) != strs[j-1].charAt(i)))
                return res.toString();
        }
        res.append(strs[0].charAt(i));
    }
    return res.toString();
}
```

Check the same locations' letter, if found any different letter or exceed any word's length, you can return the existed result.

**Complexity:**

* **worst-case time complexity:** `O(m * n)`, where `n` is the length of `strs`, `m` is the length of word in the `strs`.
* **worst-case space complexity:** `O(1)`.