# LC76. Minimum Window Substring

### LeetCode (Hard)

## Question

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**
```
Input: 
S = "ADOBECODEBANC", T = "ABC"

Output: 
"BANC"
```

**Note:**

* If there is no such window in S that covers all characters in T, return the empty string "".
* If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

## Solutions

### Solution 1

* Java
```
class Solution {
    
    private final int SIZE = 256;
    
    public String minWindow(String s, String t) {
        int[] source = new int[SIZE];
        int[] target = getTargetMap(t);
        char[] sChar = s.toCharArray();
        int minWindow = Integer.MAX_VALUE;
        int minStart = 0, j = 0;
        
        for (int i = 0; i < sChar.length; i++) {
            while (j < sChar.length && !containsAll(source, target))
                source[sChar[j++]]++;
            
            if (containsAll(source, target) && j - i < minWindow) {
                minWindow = j - i;
                minStart = i;
            }
            
            source[sChar[i]]--;
        }
        
        return minWindow == Integer.MAX_VALUE ? "" : s.substring(minStart, minStart + minWindow);
    }
    
    private int[] getTargetMap(String t) {
        int[] target = new int[SIZE];
        for (char c : t.toCharArray())
            target[c]++;
        return target;
    }
    
    private boolean containsAll(int[] source, int[] target) {
        for (int i = 0; i < SIZE; i++)
            if (source[i] < target[i])
                return false;
        return true;
    }
}
```

1. Two loops
2. No need to put `j` back.

**NOTE**

* There could be no such window in S.
* Use two hashmap is the key.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is length of `s`.
* **worst-case space complexity:** `O(1)`.
