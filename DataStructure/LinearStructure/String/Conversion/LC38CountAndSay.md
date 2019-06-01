# LC38. Count and Say

### LeetCode

## Question

The count-and-say sequence is the sequence of integers beginning as follows:

```
1, 11, 21, 1211, 111221, ...
1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.
```

Given an integer n, generate the nth sequence.

**Note:** The sequence of integers will be represented as a string.

## Solutions

### Solution 1

* C++1 (3ms)
```
string countAndSay(int n) {
    string res = "1";
    for(int i=2; i<=n; ++i)
    {
        string aRow="";
        int count = 1;
        for(int j=1; j<res.size(); ++j)
        {
            if(res[j]== res[j-1]) count++;
            else
            {
                aRow+=to_string(count)+res[j-1];
                count=1;
            }
        }
        aRow += to_string(count)+res[res.length()-1];
        res = aRow;
    }
    return res;
}
```

* C++ (4ms)
```
string countAndSay(int n) {
    string s = "1", sub;
    for(int i=1; i<n; i++)
    {
        int count =1, len = s.size() - 1 ;
        for(int j=0; j<len; j++)
        {
            if(s[j] == s[j+1])
            {
                count++;
            }
            else
            {
                sub += to_string(count) + s[j];
                count = 1;
            }
        }
        sub += to_string(count) + s[len];
        s = sub;
        sub="";
    }
    return s;
}
```

* Java (6ms)
```
public String countAndSay(int n) {
    String s = "1";
    for(int i=1; i<n; ++i)
    {
        StringBuilder sb = new StringBuilder();
        for(int j=1, count=1; j<=s.length(); ++j)
        {
            if(j==s.length() || s.charAt(j-1)!=s.charAt(j))
            {
                sb.append(count);
                sb.append(s.charAt(j-1));
                count=1;
            }
            else 
                count++;
        }
        s = sb.toString();
    }
    return s;
}
```

Step by step count the digits. Be carefull the last count.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>).
* **worst-case space complexity:** `O(n)`.