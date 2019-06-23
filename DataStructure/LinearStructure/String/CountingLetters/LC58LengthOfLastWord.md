# LC58. Length of Last Word

### LeetCode

## Question

Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return 0.

Note: A word is defined as a character sequence consists of non-space characters only.

**For example** 
```
Given s = "Hello World",
return 5.
```

## Solutions

### Solution 1

* C++ (5ms)
```
int lengthOfLastWord(string s) {
    int count=1, last=s.find_last_not_of(' ');
    if(last<0) return 0;
    while(last-->0)
    {
        if(s[last] != ' ') count++;
        else return count;
    }
    return count;
}
```

One trick of this question is that the input string could have ending empty space.

This solution is to count letters starting from the index of the last not empty space.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.

### Solution 2

* C++ (4ms)
```
int lengthOfLastWord(string s) {
    int count = 0;
    for(int i= s.size()-1; i>=0; i--)
    {
        if(isalpha(s[i])) count++;
        else if(count == 0) continue;
        else return count;
    }
    return count;
}
```

Using `if(count == 0)` to skip the ending empty space problem.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.

### Solution 3

* Java (0ms)
```
public int lengthOfLastWord(String s) {
    s = s.trim();
    int i = s.length()-1;
    for(; i>=0; --i)
        if(s.charAt(i) == ' ') break;  // if(!Character.isLetter(s.charAt(i)))  
    return s.length()-i-1;
}
```

Java String has to `trim()` method can solve the ending empty space problem.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.