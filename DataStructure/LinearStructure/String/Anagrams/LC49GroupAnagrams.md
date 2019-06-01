# LC49. Group Anagrams

### LeetCode

## Question

Given an array of strings, group anagrams together.

**For example** 
```
given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
Return:
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:** All inputs will be in lower-case.

## Solutions

### Solution 1

* C++
```
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    vector<vector<string>> res;
    unordered_map<string, int> map;
    for(string str : strs)
    {
        string subStr = str;
        sort(subStr.begin(),subStr.end());
        if(map.count(subStr)==0)
        {
            res.push_back(vector<string>(1, str));
            map[subStr] = res.size()-1;
        }
        else
            res[map[subStr]].push_back(str);
    }
    return res;
}
```

* C++
```
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    vector<vector<string>> res;
    if(strs.empty()) return res;
    string s;
    unordered_map<string, multiset<string>> groups;
    for(string str : strs)
    {
        s = str;
        sort(s.begin(), s.end());
        groups[s].insert(str);
    }
    for(auto g : groups)
    {
        vector<string> arow(g.second.begin(), g.second.end());
        res.push_back(arow);
    }
    return res;
}
```

Using the sorted string as key, store the strings to a map.

**Complexity:**

* **worst-case time complexity:** `O(n * m * log(m))`, where `n` is the length of the input `strs`, `m` is the maximum legth of the string in the `strs`.
* **worst-case space complexity:** `O(max(n, log(m)))`, where `n` is the length of the input `strs`, `m` is the maximum legth of the string in the `strs`.