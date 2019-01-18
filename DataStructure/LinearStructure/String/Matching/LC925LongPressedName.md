# LC925. Long Pressed Name

### LeetCode

## Question

Your friend is typing his name into a keyboard.  Sometimes, when typing a character c, the key might get long pressed, and the character will be typed 1 or more times.

You examine the typed characters of the keyboard.  Return True if it is possible that it was your friends name, with some characters (possibly none) being long pressed.

**Example 1:**
```
Input: name = "alex", typed = "aaleex"
Output: true
Explanation: 'a' and 'e' in 'alex' were long pressed.
```

**Example 2:**
```
Input: name = "saeed", typed = "ssaaedd"
Output: false
Explanation: 'e' must have been pressed twice, but it wasn't in the typed output.
```

**Example 3:**
```
Input: name = "leelee", typed = "lleeelee"
Output: true
```

**Example 4:**
```
Input: name = "laiden", typed = "laiden"
Output: true
Explanation: It's not necessary to long press any character.
```

**Note:**

* name.length <= 1000
* typed.length <= 1000
* The characters of name and typed are lowercase letters.

## Solutions

* Java1
```
class Solution {
    public boolean isLongPressedName(String name, String typed) {
        int n=0, t=0;
        while(n<name.length() && t<typed.length()){
            if(name.charAt(n) != typed.charAt(t)) return false;
            int n2 = indexOfNextLetter(name, n+1);
            int t2 = indexOfNextLetter(typed, t+1);
            if(n2-n > t2-t) return false;
            n = n2;
            t = t2;
        }
        return n==name.length() && t==typed.length();
    }
    
    private int indexOfNextLetter(String str, int i){
        while(i<str.length() && str.charAt(i) == str.charAt(i-1)) i++;
        return i;
    }
}
```

## Explanation

Count the number of each letter. The number of the name's letter should be less or equal than the number of typed's letter

* **worst-case time complexity:** `O(max(N,M))`, where `N` and `M` are the lengths of the input String `name` and `typed`.
* **worst-case space complexity:** `O(1)`.
