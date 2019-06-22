# LC171. Excel Sheet Column Number

### LeetCode

## Question

Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

**For example:**

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
```

## Solutions

### Solution 1

* C++ (6ms)
```
int titleToNumber(string s) {
    int res=0;
    for(int i=0; i<s.length(); ++i)
        res = res*26 + toupper(s[i])-'A'+1;
    return res;
}
```

It's like a base 26 system.

**Note** 

* it's starting from `1`.
* Ask what should return if res is larger than MAX_INT.


**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.