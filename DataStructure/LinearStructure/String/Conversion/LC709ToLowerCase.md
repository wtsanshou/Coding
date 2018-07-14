# LC709. To Lower Case

### LeetCode

## Question

Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

## Solutions

* Java1
```
class Solution {
    
    private static final int DIS = 'a' - 'A';
    
    public String toLowerCase(String str) {
        char[] strs = str.toCharArray();
        for(int i=0; i<strs.length; ++i)
            if(Character.isUpperCase(strs[i])) strs[i] += DIS;
        return new String(strs);
    }
}
```

## Explanation

* **worst-case time complexity:** `O(n)`, where `n` is the length of the String `str`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the String `str`.
