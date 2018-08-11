# LC844. Backspace String Compare

### LeetCode

## Question

Given two strings `S` and `T`, return if they are equal when both are typed into empty text editors. `#` means a backspace character.

**Example 1:**
```
Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
```

**Example 2:**
```
Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
```

**Example 3:**
```
Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
```

**Example 4:**
```
Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
```

**Note:**

* 1 <= S.length <= 200
* 1 <= T.length <= 200
* S and T only contain lowercase letters and `#` characters.

**Follow up:**

Can you solve it in O(N) time and O(1) space?

## Solutions

* Scala1
```
object Solution {
    def backspaceCompare(S: String, T: String): Boolean = {
        getText(S) == getText(T)
    }
    
    def getText(s: String): scala.collection.mutable.Stack[Char] = {
        var res = new scala.collection.mutable.Stack[Char]
        s.foreach(c => c match{
            case '#' => if(!res.isEmpty) res.pop
            case _ => res.push(c)
        })
        res
    }
}
```

## Explanation

The stack is the best solution for this question.

* **worst-case time complexity:** O(max(N,M)), where `N` and `M` are the lengths of the input String `S` and `T`.
* **worst-case space complexity:** O(max(N,M)), where `N` and `M` are the lengths of the input String `S` and `T`.
