# LC680. Valid Palindrome II

Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.

**Example 1:**

```
Input: "aba"
Output: True
```

**Example 2:**

```
Input: "abca"
Output: True
```

**Explanation:** 

You could delete the character 'c'.

**Note:**

The string will only contain lowercase characters a-z. The maximum length of the string is 50000.

## Solutions

* C#1 (Runtime Error)
```
public class Solution {
    
    private bool first = true;
    
    public bool ValidPalindrome(string s) {
        return RecurPalindrome(s, 0, s.Length-1);
    }
    
    private bool RecurPalindrome(string s, int left, int right){
        if(left >= right) return true;
        if(s[left] != s[right]){
            if(first){
                first = false;
                return RecurPalindrome(s, left+1, right) || RecurPalindrome(s, left, right-1);
            }
            return false;
        }
        return RecurPalindrome(s, left+1, right-1);
    }
}
```

* C#2
```
public class Solution {
    
    private bool first;
    
    public bool ValidPalindrome(string s) {
        first = true;
        return RecurPalindrome(s, 0, s.Length-1);
    }
    
    private bool RecurPalindrome(string s, int left, int right){
        for(; left < right; left++, right--){
            if(s[left] != s[right]){
                if(first){
                    first = false;
                    return RecurPalindrome(s, left+1, right) || RecurPalindrome(s, left, right-1);
                }
                return false;
            }
        }
        return true;
    }
}
```

## Explanation

I like the recursive solution, but it might take too much memory?

It's a Greedy algorithm.

The idea is when found the first non-equal letters, try to ignore one of the letters.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)