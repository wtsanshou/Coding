# LC796. Rotate String

### LeetCode

## Question

We are given two strings, A and B.

A shift on A consists of taking string A and moving the leftmost character to the rightmost position. For example, if A = 'abcde', then it will be 'bcdea' after one shift on A. Return True if and only if A can become B after some number of shifts on A.

**Example 1:**
```
Input: A = 'abcde', B = 'cdeab'
Output: true
```

**Example 2:**
```
Input: A = 'abcde', B = 'abced'
Output: false
```

**Note:**

A and B will have length at most `100`.

## Solutions

* Java1

```
class Solution {
    public boolean rotateString(String A, String B) {
        int n = A.length();
        if(n != B.length()) return false;
        for(int i=0; i<n; ++i){
            if(rotatable(A, B, i)) return true;
        }
        return false;
    }    
    private boolean rotatable(String A, String B, int start){
        for(int i=start; i<A.length()+start; ++i){
            if(A.charAt(i%A.length()) != B.charAt(i-start)) return false;
        }
        return true;
    }
}
```

## Explanation

Starting from each letter of the String `A`, compare them with the String `B` which is always starting from beginning. When reach the end of the String `A`, continue from the beginning of the String `A`.

* **worst-case time complexity:** O(N<sup>2<sup>), where `N` is the size of the input String `A` or `B`
* **worst-case space complexity:** O(1)