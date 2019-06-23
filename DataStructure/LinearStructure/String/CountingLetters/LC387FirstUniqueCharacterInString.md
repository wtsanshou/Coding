# LC387. First Unique Character in a String

### LeetCode

## Question

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

**Note:** You may assume the string contain only lowercase letters.

## Solutions

### Solution 1

* C++ (42ms)
```
int firstUniqChar(string s) {
    int count[128] = {0};
    for(char c : s)
        count[c]++;
    for(int i=0; i<s.length(); ++i)
        if(count[s[i]] == 1) return i;
    return -1;
}
```

Using a map `count` to remember the number of each letter in `s`.

Travesal the string `s` again, the first letter with count `1` is the result.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.