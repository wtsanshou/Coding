# LC1021. Remove Outermost Parentheses

### LeetCode

## Question

A valid parentheses string is either empty (""), "(" + A + ")", or A + B, where A and B are valid parentheses strings, and + represents string concatenation.  For example, "", "()", "(())()", and "(()(()))" are all valid parentheses strings.

A valid parentheses string S is primitive if it is nonempty, and there does not exist a way to split it into S = A+B, with A and B nonempty valid parentheses strings.

Given a valid parentheses string S, consider its primitive decomposition: S = P_1 + P_2 + ... + P_k, where P_i are primitive valid parentheses strings.

Return S after removing the outermost parentheses of every primitive string in the primitive decomposition of S.

**Example 1:**
```
Input: "(()())(())"
Output: "()()()"
Explanation: 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```

**Example 2:**
```
Input: "(()())(())(()(()))"
Output: "()()()()(())"
Explanation: 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
```

**Example 3:**
```
Input: "()()"
Output: ""
Explanation: 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".
```

**Note:**

* S.length <= 10000
* S[i] is "(" or ")"
* S is a valid parentheses string

## Solutions

### Solution 1

* Java
```
class Solution {
    public String removeOuterParentheses(String S) {
        int id = findIdOfPrimitive(S);
        String left = (id>2) ? S.substring(1,id-1) : "";
        return left + ((id<S.length()) ? removeOuterParentheses(S.substring(id)) : "");
    }
    
    private int findIdOfPrimitive(String S){
        int alart = 0;
        for(int i=0; i<S.length(); i++){
            if(S.charAt(i)=='(') alart++;
            else alart--;
            if(alart==0) return i+1;
        }
        return 0;
    }
}
```

Find the first primitive substring and remove the outer of it. Recursive the rest substring of the input.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input String `S`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input String `S`.

### Solution 2

* Java
```
public String removeOuterParentheses(String S) {
    int open = 0;
    StringBuilder sb = new StringBuilder();
    for(char c : S.toCharArray()){
        if(c == '('){
            open++;
            if(open > 1) sb.append(c);
        }
        else{
            open--;
            if(open > 0) sb.append(c);
        }
    }
    return sb.toString();
}
```

Iterative append each primitive.

Avoid two outers:

1. `c=='(' && open==1` -- open Parentheses
2. `c==')' && open==0` -- close Parentheses

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input String `S`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input String `S`.
