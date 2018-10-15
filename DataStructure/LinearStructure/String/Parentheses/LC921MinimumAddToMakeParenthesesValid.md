# LC921. Minimum Add to Make Parentheses Valid

### LeetCode

## Question

Given a string S of '(' and ')' parentheses, we add the minimum number of parentheses ( '(' or ')', and in any positions ) so that the resulting parentheses string is valid.

Formally, a parentheses string is valid if and only if:

It is the empty string, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.
Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.

**Example 1:**
```
Input: "())"
Output: 1
```

**Example 2:**
```
Input: "((("
Output: 3
```

**Example 3:**
```
Input: "()"
Output: 0
```

**Example 4:**
```
Input: "()))(("
Output: 4
``` 

**Note:**

* S.length <= 1000
* S only consists of '(' and ')' characters.

## Solutions

* Scala1
```
def minAddToMakeValid(S: String): Int = {
    var (a,b) = (0,0)
    S.foreach(s =>{
        s match {
            case '(' => a=a+1
            case ')' => if(a==0) b=b+1 else a=a-1
        }
    })
    a+b
}
```

## Explanation

Using a integer `a` as a stack to store `(`.

When meet a `)`, if the stack `a` is empty (`a==0`), accumulate the number of the `)`; else pop one `(` from the stack `a`.

* **worst-case time complexity:** O(n), where `n` is the length of the String `S`.
* **worst-case space complexity:** O(1)

