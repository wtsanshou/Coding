# Lint780. Remove Invalid Parentheses

### LintCode (Hard)

## Question

Remove the minimum number of invalid parentheses in order to make the input string valid. Return all possible results.

**Example 1:**
```
Input:
"()())()"
Ouput:
["(())()","()()()"]
```

**Example 2:**
```
Input:
"(a)())()"
Output:
 ["(a)()()", "(a())()"]
```

**Example 3:**
```
Input:
")(" 
Output:
 [""]
```

**Notice**

* The input string may contain letters other than the parentheses `(` and `)`.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param s: The input string
     * @return: Return all possible results
     */
     
    private char[][] patterns = { {'(', ')'}, {')', '('} };
    
    public List<String> removeInvalidParentheses(String s) {
        List<String> res = new ArrayList<>();
        dfs(s, 0, 0, patterns[0], res);
        return res;
    }
    
    private void dfs(String s, int start, int lastRemove, char[] pattern, List<String> res) {
        int count = 0, n = s.length();
        
        for (int i = start; i < n; i++) {
            if (s.charAt(i) == pattern[0]) // ignore letter
            { 
                count++;
            }
            if (s.charAt(i) == pattern[1]) // ignore letter
            { 
                count--;
            }
            
            if (count < 0) {
                for (int j = lastRemove; j <= i; j++) {
                    if (s.charAt(j) == pattern[1] && (j == lastRemove || s.charAt(j) != s.charAt(j - 1))) {
                        dfs(s.substring(0, j) + s.substring(j + 1), i, j, pattern, res); // the char at `j` is removed.
                    }
                }
                return;
            }
        }
        
        s = new StringBuilder(s).reverse().toString();
        if (pattern[0] == patterns[0][0]) { // first pattern check finished
            dfs(s, 0, 0, patterns[1], res);
        } else { // it's the second check
            res.add(s);
        }
    }
}
```

This parentheses question is not able to use `Stack` to solve.

The question asks for `Return all possible results`. It is likely to be `DFS` solution. 

The idea is to use `count` to check if the substring from `start` to `i` is valid:

If `count < 0`, it means the number of `pattern[1]` is more than the number of `pattern[0]`. We need to remove a `pattern[1]` in the substring. 

Some corner cases here:

1. Only one `pattern[1]` need to be removed in the contiguous `pattern[1]`s.
2. The `pattern[1]` before the `lastRemove` does not need to check anymore, because they have already proceed.
3. the char at `j` is removed.
4. When found an invalid (`count < 0`), need to return. Only go to the second check when it pass the first check.

THe first `patterns[0]` check can only make sure the number of `(` is more than the number of `)`. So we need the second `patterns[1]` check to make sure the the number of `)` is more than the number of `(`. So that the number of `(` equals to the number of `)`.

For the scond `patterns[1]` checking, we reverse the original input. So we can reuse the `dfs` function for the `patterns[1]`.

**Complexity:**

* **worst-case time complexity:** Hard to say, maybe `O(n!)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.

