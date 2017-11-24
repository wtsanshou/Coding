# LC696. Count Binary Substrings

### LeetCode

## Question

Give a string s, count the number of non-empty (contiguous) substrings that have the same number of 0's and 1's, and all the 0's and all the 1's in these substrings are grouped consecutively.

Substrings that occur multiple times are counted the number of times they occur.

**Example 1:**

```
Input: "00110011"
Output: 6
```

**Explanation:**

There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".

Notice that some of these substrings repeat and are counted the number of times they occur.

Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.

**Example 2:**

```
Input: "10101"
Output: 4
```

**Explanation:**

There are 4 substrings: "10", "01", "10", "01" that have equal number of consecutive 1's and 0's.

**Note:**

* s.length will be between 1 and 50,000.
* s will only consist of "0" or "1" characters.

## Solutions

* Java1
```
class Solution {
    public int countBinarySubstrings(String s) {
        int res = 0;
        for(int i=0; i<s.length()-1; ++i)
            res += countBinaryAt(s, i);
        return res;
    }
    
    private int countBinaryAt(String s, int n){
        int res = 0;
        for(int i=n, j=n+1; i>=0 && j<s.length(); --i, ++j){
            if(s.charAt(i) == s.charAt(j) || 
               s.charAt(i) != s.charAt(n) ||
               s.charAt(j) != s.charAt(n+1))
                return res;
            res++;
        }
        return res;
    }
}
```

## Explanation

**Non equal** number of consecutive 1's and 0's:

1. `s.charAt(i) == s.charAt(j)`
2. `s.charAt(i) != s.charAt(n)`
3. `s.charAt(j) != s.charAt(n+1)`

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)

