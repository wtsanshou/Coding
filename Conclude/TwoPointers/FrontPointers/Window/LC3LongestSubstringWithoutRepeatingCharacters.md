# LC3. Longest Substring Without Repeating Characters

### LeetCode (medium)

## Question

Given a string, find the length of the longest substring without repeating characters.

**Example 1:**
```
Input: 
"abcabcbb"

Output: 
3 

Explanation: 
The answer is "abc", with the length of 3. 
```

**Example 2:**
```
Input: 
"bbbbb"

Output: 
1

Explanation: 
The answer is "b", with the length of 1.
```

**Example 3:**
```
Input: 
"pwwkew"

Output: 
3

Explanation: 
The answer is "wke", with the length of 3. 
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## Solutions

## Solution 1

* Java
```
class Solution {
    public int lengthOfLongestSubstring(String s) {
        boolean[] map = new boolean[256];
        int j = 0, res = 0;
        char[] chars = s.toCharArray();
        
        for (int i = 0; i < chars.length; i++) {
            while (j < chars.length && map[chars[j]] == false)
                 map[chars[j++]] = true;
            res = Math.max(res, count(map));
            map[chars[i]] = false;
        }
        
        return res;
    }
    
    private int count(boolean[] map) {
        int res = 0;
        
        for (boolean m : map)
            if (m)
                res++;
        
        return res;
    }
}
```

1. Two loop.
2. No need to put `j` back.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is length of `s`.
* **worst-case space complexity:** `O(1)`.
