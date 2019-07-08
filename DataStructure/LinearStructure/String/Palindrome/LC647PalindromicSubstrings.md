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

### Solution 1

* C++
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
        for(int i=1; i<n-1; ++i) // starting from 1, so you missed checking s[0]==s[1] we can start from 0!!! test it
            res += countPalindrom(i, s);
        return n+res + ((n>0 && s[0]==s[1]) ? 1 : 0); 
    }
};
```

Each single letter is a palindrome, so `n` is part of the result. Then we just need to count palindrome with length of more than `1` starting from each character in the `s`.

One corner case: 

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `x`.  
* **worst-case space complexity:** `O(1)`.

* Java
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

* Java
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





* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)
