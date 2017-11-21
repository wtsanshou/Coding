# LC168. Excel Sheet Column Title

### LeetCode

## Question

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
```

## Solutions

* C++1(0ms)
```
string convertToTitle(int n) {
    string res = "";
    while(n>0)
    {
        res = (char)('A' - 1 + ((n%26 == 0)? 26: n%26)) + res;
        n = n/26 - ((n%26 == 0)? 1 : 0);
    }
    return res;
}
```

* C++2 (0ms)
```
string convertToTitle(int n) {
    if(n==0) return "";
    return convertToTitle((n-1)/26) + (char)('A' + (n-1)%26);
}
```

* C++3
```
string convertToTitle(int n) {
        string res = "";
        while(n>0)
        {
            res = (char)('A' + (n-1)%26) + res;
            n = (n-1)/26;
        }
        return res;
}
```

* Java1
```
public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while(n>0)
        {
            sb.insert(0, (char)('A' +(n-1)%26));
            n = (n-1) / 26;
        }
        return sb.toString();
    }
```

## Explanation

**NOTE** 

1. `res = (char)('A' + (n-1)%26) + res;`
2. `n = (n-1)/26;`

* **worst-case time complexity:** O(log<sub>26</sub>(n))
* **worst-case space complexity:** O(1)
