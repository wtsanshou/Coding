# LC616. Add Bold Tag in String

### LeetCode

## Question

Given a string s and a list of strings dict, you need to add a closed pair of bold tag `<b>` and `</b>` to wrap the substrings in s that exist in dict. If two such substrings overlap, you need to wrap them together by only one pair of closed bold tag. Also, if two substrings wrapped by bold tags are consecutive, you need to combine them.

**Example 1:**

**Input:** 
```
s = "abcxyz123"
dict = ["abc","123"]
```

**Output:**

`<b>abc</b>xyz<b>123</b>`

**Example 2:**

**Input:** 
```
s = "aaabbcc"
dict = ["aaa","aab","bc"]
```

**Output:**

`<b>aaabbc</b>c`

**Note:**

The given dict won't contain duplicates, and its length won't exceed 100.

All the strings in input have length in range [1, 1000].


## Solutions

* C++1
```
int searchMaxLen(string& s, int start, vector<string> words)
{
    int len = 0;
    for(string w : words)
    {
        int wl = w.length();
        if(start+wl<=s.length() && s.substr(start, wl)==w)
            len = max(len, wl);
    }
    return len;
}

string addBoldTag(string s, vector<string>& dict) {
    unordered_map<char, vector<string>> wdict;
    for(string word : dict)
    {
        wdict[word[0]].push_back(word);
    }
    
    for(int i=0; i<s.length(); ++i)
    {
        if(wdict.count(s[i]) == 0) continue;
        int len = searchMaxLen(s, i, wdict[s[i]]);
        if(len == 0) continue;
        for(int j=i+1; j<=i+len; ++j)
        {
            int curLen = searchMaxLen(s, j, wdict[s[j]]);
            len = max(len, j-i + curLen);
        }
        s.insert(i+len, "</b>");
        s.insert(i, "<b>");
        i += len+7;
    }
    return s;
}
```

## Explanation

Map all the dict words to their first character. 

Based on the first character, if we found a maxmum length (**LEN**) word in the dictionary, it means we need to insert a bold tag `<b>` and `</b>`.

Keep searching in this **LEN** and a character after this range. If we can find a dict word which could increase the **LEN**, increase the searching range entil we cannot find a dict word in the legal range.

Insert `</b>` first, because it won't affect the insert location of `<b>`.

