# LC917. Reverse Only Letters

### LeetCode

## Question

Given a string S, return the "reversed" string where all characters that are not a letter stay in the same place, and all letters reverse their positions.

**Example 1:**
```
Input: "ab-cd"
Output: "dc-ba"
```

**Example 2:**
```
Input: "a-bC-dEf-ghIj"
Output: "j-Ih-gfE-dCba"
```

**Example 3:**
```
Input: "Test1ng-Leet=code-Q!"
Output: "Qedo1ct-eeLg=ntse-T!"
```

**Note:**

* S.length <= 100
* 33 <= S[i].ASCIIcode <= 122 
* S doesn't contain \ or "

## Solutions

* Scala1
```
def reverseOnlyLetters(S: String): String = {
    var letters = S.filter(_.isLetter)
    S.map(c => if(c.isLetter){
        val letter = letters.last
        letters = letters.dropRight(1)
        letter
    }else c )
}
```

## Explanation

Filter in all letters. Map letters in reverse order.

* **worst-case time complexity:** O(n), where `n` is size of the String `S`.
* **worst-case space complexity:** O(n), where `n` is size of the String `S`.
