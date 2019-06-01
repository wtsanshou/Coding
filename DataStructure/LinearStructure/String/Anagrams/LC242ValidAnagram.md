# LC242. Valid Anagram

### LeetCode

## Question

Given two strings s and t, write a function to determine if t is an anagram of s.

**For example**
```
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.
```

**Note:**

* You may assume the string contains only lowercase alphabets.

**Follow up:**

What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Solutions

### Solution 1

* C++ (76ms)
```
bool isAnagram(string s, string t) {
    int lens = s.length();
    int lent = t.length();
    if(lens != lent)  return false;
    sort(s.begin(), s.end());
    sort(t.begin(), t.end());
    for(int i=0; i<lens; i++)
        if(s[i] != t[i])
            return false;
    return true;
}
```

Sort both string `s` and `t`. Should be the same if they are anagram.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.

### Solution 2

* C++ (13ms)
```
bool isAnagram(string s, string t) {
    int sLen = s.length();
    if(sLen != t.length()) return false;
    int count[128] = {0};
    for(int i=0; i<sLen; ++i)
        count[s[i]]++;
    for(char c : t)
        if(--count[c] < 0) return false;
    return true;
}
```

* Java (3ms)
```
public boolean isAnagram(String s, String t) {
    int n = s.length();
    if(n != t.length()) return false;
    int[] alp = new int[26];
    for(int i=0; i<n; ++i)
    {
        alp[s.charAt(i)-'a']++;
        alp[t.charAt(i)-'a']--;
    }
    for(int a : alp)
    {
        if(a!=0) return false;
    }
    return true;
 }
```

Count the number of each letter in `s` and `t`. Both should have the same number of each letter if they are anagram.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.