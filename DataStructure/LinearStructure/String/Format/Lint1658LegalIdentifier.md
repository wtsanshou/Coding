# Lint1658. Legal Identifier

### LintCode

## Question

Please judge if string str is a valid identifier.

Legal identifiers consist of letters (A-Z, a-z), numbers (0-9) and underscores, and the first character cannot be a number.

**Example 1**:
```
Input: str = "LintCode"
Output: true

Explanation:
Because 'LintCode' is consist of letters.
```

**Example 2:**
```
Input: str = "123_abc"
Output: false

Explanation:
Through '123_abc' is consist of letters, numbers and underscores, but its' first character is number.
```

## Solutions

### Solution 1

* Java
```
public boolean isLegalIdentifier(String str) {
    if(str==null || str.isEmpty()) return false;
    if(!Character.isLetter(str.charAt(0)) && str.charAt(0)!='_') return false;
    for(char c : str.toCharArray()){
        if(c!='_' && !Character.isLetterOrDigit(c)) 
            return false;
    }
    return true;
}
```

Clear the requirements: 

1. Only letter, digit, and underscore are legal in the string.
2. Letter or underscore could be the first character.
3. Empty string is not legal.

So, we just need to clean all the corner cases:

1. `str` is null.
2. `str` is empty.
3. First character is neither letter nor underscore.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `str`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `str`.
