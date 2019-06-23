# LC482. License Key Formatting

### LeetCode

## Question

Now you are given a string S, which represents a software license key which we would like to format. The string S is composed of alphanumerical characters and dashes. The dashes split the alphanumerical characters within the string into groups. (i.e. if there are M dashes, the string is split into M+1 groups). The dashes in the given string are possibly misplaced.

We want each group of characters to be of length K (except for possibly the first group, which could be shorter, but still must contain at least one character). To satisfy this requirement, we will reinsert dashes. 
Additionally, all the lower case letters in the string must be converted to upper case.

So, you are given a non-empty string S, representing a license key to format, and an integer K. And you need to return the license key formatted according to the description above.

**Example 1:**

```
Input: S = "2-4A0r7-4k", K = 4

Output: "24A0-R74K"

Explanation: The string S has been split into two parts, each part has 4 characters.
```

**Example 2:**

```
Input: S = "2-4A0r7-4k", K = 3

Output: "24-A0R-74K"

Explanation: The string S has been split into three parts, each part has 3 characters except the first part as it could be shorter as said above.
```

**Note:**

1.	The length of string S will not exceed 12,000, and K is a positive integer.
2.	String S consists only of alphanumerical characters (a-z and/or A-Z and/or 0-9) and dashes(-).
3.	String S is non-empty.

## Solutions

### Solution 1

* C++ (53ms)
```
string licenseKeyFormatting(string S, int K) {
    int j=1, n=S.length();
    string res;
    while(j <= n)
    {
        int i = n-j;
        if(S[i] == '-') 
        {
            j++;
            continue;
        }
        if(isalpha(S[i])) S[i] = toupper(S[i]);
        res = S[i] + res;
        if(++j<=n && res.length()%(K+1)==K) res = '-' + res;
    }
    return res[0]=='-' ? res.substr(1) : res;
}
```

* C++ (46ms)
```
string licenseKeyFormatting(string S, int K) {
    string res;
    for(int i=S.length()-1; i>=0; --i)
    {
        if(S[i] != '-') 
        {
            if(isalpha(S[i])) S[i] = toupper(S[i]);
            res = S[i] + res;
            if(res.length()%(K+1)==K) res = '-' + res;
        }
    }
    return res[0]=='-' ? res.substr(1) : res;
}
```

Build the license key from right to left.

Put `-` based on the length of the result string.

**Note** You may put a '-' at the beginning of your result when the length of the first key is equal to `K`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `S`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* Java
```
class Solution {
    public String licenseKeyFormatting(String S, int K) {
        String input = S.replaceAll("-", "");
        String upperInput = convertToUppercase(input);
        
        int n = upperInput.length();
        if(n==0) return ""; //the input could be "-----"
        
        int first = n % K;
        if(first==0) {
            first = K;    
        }
        
        StringBuilder sb = new StringBuilder();
        sb.append(upperInput.substring(0,first));
        
        for(int start=first; start<n; start+=K){
            sb.append("-"+upperInput.substring(start,start+K));
        }
        return sb.toString();
    }
    
    private String convertToUppercase(String input){
        char[] strs = input.toCharArray();
        for(int i=0; i<strs.length; i++)
            if(Character.isLetter(strs[i]))
                strs[i] = Character.toUpperCase(strs[i]);
        return new String(strs);
    }
}
```

Build the license key from left to right.

First, I cleaned up the input `S`: remove all '-' and convert all letters to upper case.

Using `n % K` to find the length of the first key. After the first key, all rest keys are `"-"+key`.

**NOTE** a corner case is that the input are all `-` which could case problem when we try to build the first key.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `S`.
* **worst-case space complexity:** `O(1)`.
