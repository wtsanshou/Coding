# LC647. Palindromic Substrings

### LeetCode

## Question

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

**Example 2:**
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

**Note:**

1.  The input string length won't exceed 1000.

## Solutions

* C++1
```
class Solution {
public:
    int countFrom(int i, int j, string & s)
    {
        int c = 0;
        while(i>=0 && j<s.length() && s[i--]==s[j++])
            c++;
        return c;
    }
    
    int countPalindrom(int i, string& s)
    {
        int c = 0;
        c += countFrom(i-1, i+1, s);
        c += countFrom(i, i+1, s);
        return c;
    }
    
    int countSubstrings(string s) {
        int res = 0, n = s.length();
        for(int i=1; i<n-1; ++i)
            res += countPalindrom(i, s);
        return n+res + ((n>0 && s[0]==s[1]) ? 1 : 0);
    }
};
```

* Java1
```
public int countSubstrings(String s) {
        int res=0, n=s.length();
        for(int i=1; i<n-1; ++i){
            int temp = 0;
            int left=i-1, right=i+1;
            while(left>=0 && right<n && s.charAt(left--)==s.charAt(right++))
                temp++;
            left=i;
            right=i+1;
            while(left>=0 && right<n && s.charAt(left--)==s.charAt(right++))
                temp++;
            res += temp;
        }
        return n+res + ((n>1 && s.charAt(0)==s.charAt(1)) ? 1 : 0);
}
```

* Java2
```public int countSubstrings(String s) {
        int res=0, n=s.length();
        char[] cs = s.toCharArray();
        for(int i=1; i<n-1; ++i){
            int temp = 0;
            int left=i-1, right=i+1;
            while(left>=0 && right<n && cs[left--]==cs[right++])
                temp++;
            left=i;
            right=i+1;
            while(left>=0 && right<n && cs[left--]==cs[right++])
                temp++;
            res += temp;
        }
        return n+res + ((n>1 && cs[0]==cs[1]) ? 1 : 0);
}
```

## Explanation

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)
