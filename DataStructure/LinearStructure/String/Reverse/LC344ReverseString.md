# LC344. Reverse String

### LeetCode

## Question

Write a function that takes a string as input and returns the string reversed.

**Example:**
```
Given s = "hello", 
return "olleh".
```

## Solutions

### Solution 1

* C++
```
string reverseString(string s) {
    int i = 0, j = s.size() - 1;
    while(i < j){
        swap(s[i++], s[j--]); 
    }
    return s;
}
```

* C++
```
string reverseString(string s) {
    int len = s.size();
    for(int i=0; i<len/2; i++)
        swap(s[i], s[len-i-1]);
    return s;
}
```

* Java
```
public String reverseString(String s) {
    int n = s.length();
    StringBuilder sb= new StringBuilder();
    char[] c = s.toCharArray();
    for(int i=n-1; i>=0; --i)
        sb.append(c[i]);
    return sb.toString();
}
```

* Python
```
def reverseString(self, s):
    return s[::-1]
```

This is a classic question. The key of this question is its follow up:

1. What if `s` is null?
2. What if it has space?
3. What if it has other characters instead of only letters?

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.
