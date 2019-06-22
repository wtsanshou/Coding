# LC205. Isomorphic Strings

### LeetCode

## Question

Given two strings s and t, determine if they are isomorphic.

Two strings are isomorphic if the characters in s can be replaced to get t.

All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

**For example**
```
Given "egg", "add", return true.
Given "foo", "bar", return false.
Given "paper", "title", return true.
```

**Note:**

* You may assume both s and t have the same length.

## Solutions

### Solution 1

* C++ (6ms)
```
bool isIsomorphic(string s, string t) {
        int Scount[128] = {0}, Tcount[128] = {0};
        if(s.length()!=t.length()) return false;
        for(int i=0; i<s.length(); ++i)
        {
            if(Scount[s[i]] != Tcount[t[i]]) return false;
            if(Scount[s[i]] == 0)
                Scount[s[i]] = Tcount[t[i]] = i+1;
        }
        return true;
}
```

* Java (5ms)
```
public boolean isIsomorphic(String s, String t) {
    char[] ss = s.toCharArray();
    char[] tt = t.toCharArray();
    int[] sAddr = new int[128];
    int[] tAddr = new int[128];
    for(int i=0; i<s.length(); ++i)
    {
        char si = ss[i], ti = tt[i];
        if(sAddr[si] != tAddr[ti]) return false;
        else if(sAddr[si] == 0)
        {
            sAddr[si] = i+1;
            tAddr[ti] = i+1;
        }
    }
    return true;
}
```

* Java (15ms)
```
public boolean isIsomorphic(String s, String t) {
    int[] sAddr = new int[256];
    int[] tAddr = new int[256];
    for(int i=0; i<s.length(); ++i)
    {
        if(sAddr[s.charAt(i)] != tAddr[t.charAt(i)]) return false;
        else
        {
            sAddr[s.charAt(i)] = i+1;
            tAddr[t.charAt(i)] = i+1;
        }
    }
    return true;
}
```

Using two array as map to remember the unique letter's location in `s` and `t`. If the location is not matched, then they are not isomorphic.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.