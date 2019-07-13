# LC28. Implement strStr

### LeetCode

## Question

Implement strStr().

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## Solutions

### Solution 1

* C++ (6ms) 
```
int strStr(string haystack, string needle) {
    int hLen=haystack.length(), nLen=needle.length();
    if(nLen>hLen) return -1;
    for(int i=0; i<=hLen-nLen; ++i)
        if(haystack.substr(i, nLen) == needle)
            return i;
    return -1;
}
```

* C++ (4ms) 
```
int strStr(string haystack, string needle) {
    int last = haystack.size()-needle.size();
    for(int i=0; i<=last; i++)
    {
        bool ok = true;
        for(int j=0; j<needle.size(); j++)
        {
            if(haystack[i+j] != needle[j])
            {
                ok = false;
                break;
            }
        }
        if(ok) return i;
    }
    return -1;
}
```

* C++ (8ms) 
```
int strStr(string haystack, string needle) {
    //if(needle.empty()) return 0;
    //if(haystack.empty() || haystack.size()<needle.size()) return -1;
    for(int i=0; ; ++i)
    {
        for(int j=0; ; ++j)
        {
            if(needle[j] == 0) return i;
            if(haystack[i+j] == 0) return -1;
            if(haystack[i+j] != needle[j]) break;
        }
    }   
}
```

* Java (1ms) 
```
public int strStr(String haystack, String needle) {
    int hLen=haystack.length(), nLen=needle.length();
    if(nLen==0) return 0;
    for(int i=0; i<=hLen-nLen; ++i)
        if(haystack.substring(i, i+nLen).equals(needle))
            return i;
    return -1;
}
```

* Java (1ms)
```
public int strStr(String haystack, String needle) {
    return haystack.indexOf(needle);
}
```

Compare the subbstring of `haystack` with `needle`.

**Note** do not ignore the last character in the `haystack`.

**Complexity:**

* **worst-case time complexity:** `O(m * n)`, where `n` is the length of `needle`, `m` is the length of the `haystack`.
* **worst-case space complexity:** `O(1)`.
