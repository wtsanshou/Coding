# LC434. Number of Segments in a String

### LeetCode

## Question

Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.

Please note that the string does not contain any non-printable characters.

## Solutions

### Solution 1

* C++ (3ms)
```
int countSegments(string s) {
    s += " ";
    int count=0;
    for(int i=1; i<s.length(); ++i)
        if(s[i] == ' ' && s[i-1]!=' ') // if(isspace(s[i]) && !isspace(s[i-1]))
            count++;
    return count;
}
```

Count the number of `non-space`+`space`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(1)`.

* C++ (0ms)
```
int countSegments(string s) {
    int count=0;
    for(int i=0; i<s.size(); ++i)
    {
        if(!isspace(s[i]))
        {
            count++;
            while(i<s.size() && !isspace(s[i]))
                i++;
        }
    }
    return count;
}
```

Find a `non-space`, count+1, skip all the adjacent `non-space`. Continue to find the next `non-space`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(1)`.