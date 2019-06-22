# LC290. Word Pattern

### LeetCode

## Question

Given a pattern and a string str, find if str follows the same pattern.
Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

**Examples:**

1.	pattern = "abba", str = "dog cat cat dog" should return true.
2.	pattern = "abba", str = "dog cat cat fish" should return false.
3.	pattern = "aaaa", str = "dog cat cat dog" should return false.
4.	pattern = "abba", str = "dog dog dog dog" should return false.

**Notes:**

You may assume pattern contains only lowercase letters, and str contains lowercase letters separated by a single space.

## Solutions

### Solution 1

* C++ (3ms)
```
class Solution {
public:
    vector<string> getWords(string str)
    {
        stringstream ss(str);
        vector<string>words;
        string token;
        while(getline(ss, token, ' '))
            words.push_back(token);
        return words;
    }
    bool wordPattern(string pattern, string str) {
        unordered_map<char, int> Pmap;
        unordered_map<string, int> Smap;
        vector<string> tokens = getWords(str);
        if(pattern.length()!= tokens.size()) return false;
        for(int i=0; i<pattern.length(); ++i)
        {
            if(Pmap[pattern[i]] != Smap[tokens[i]]) return false;
            if(Pmap[pattern[i]]==0 && Smap[tokens[i]]==0)
            {
                Pmap[pattern[i]] = i+1;
                Smap[tokens[i]] = i+1;
            }
        }
        return true;
    }
};
```

* C++ (0ms)
```
bool wordPattern(string pattern, string str) {
    unordered_map<char, int> PM;
    unordered_map<string, int> SM;
    istringstream in(str);
    int i=0, n = pattern.size();
    for(string word; in>>word; i++)
    {
        if(i==n || PM[pattern[i]] != SM[word]) return false;
        if(!PM[pattern[i]] && !SM[word])
        {
            PM[pattern[i]] = i+1;
            SM[word] = i+1;
        }
    }
    return i==n;
}
```

* Java (3ms)
```
public boolean wordPattern(String pattern, String str) {
    String[] words = str.split(" ");
    if(pattern.length() != words.length) 
        return false;
    Map addr = new HashMap();
    for(Integer i=0; i<words.length; ++i)
    {
        if(addr.put(pattern.charAt(i), i) != addr.put(words[i], i))
            return false;
    }
    return true;
}
```

Using map to remember the location of each unique letter of `pattern` and word of `str`. Matched `pattern`'s letter and `str`'s word should have the same location.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `pattern`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `pattern`.

### Wrong answer

* Java (Wrong answer)
```
public boolean wordPattern(String pattern, String str) {
    String[] words = str.split(" ");
    if(pattern.length() != words.length) 
        return false;
    Map addr = new HashMap();
    for(Integer i=0; i<words.length; ++i)
    {
        if(!addr.containsKey(pattern.charAt(i)))
            return addr.put(pattern.charAt(i), words[i])
        else if(!addr.get(pattern.charAt(i)).equals(words[i]))
            return false;
    }
    return true;
}
```

**Example**

```
"abba"
"dog dog dog dog"
```
