# LC125. Valid Palindrome

### LeetCode

## Question

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**For example**

```
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.
```

**Note:**

* Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

## Solutions

### Solution 1

* C++ (16ms)
```
bool isPalindrome(string s) {
    int i=0, j=s.length()-1;
    while(i < j)
    {
        if(!isalnum(s[i])) i++;
        else if(!isalnum(s[j])) j--;
        else
        {
            if(isalpha(s[i])) s[i] = toupper(s[i]);
            if(isalpha(s[j])) s[j] = toupper(s[j]);
            if(s[i]!=s[j]) return false;
            i++;
            j--;
        }
    }
    return true;
}
```

* C++ (14ms)
```
bool isPalindrome(string s) {
    int i=0, j=s.size()-1;
    while(i<j)
    {
        while(i<j && !isalnum(s[i])) ++i;
        while(i<j && !isalnum(s[j])) --j;
        if(isalpha(s[i]) ^ isalpha(s[j])) return false;
        int d = abs(s[i] - s[j]);
        if(d!=0 && d!=32) return false;
        ++i;
        --j;
    }
    return true;
}
```

* Java (9ms)
```
public boolean isPalindrome(String s) {
    for(int i=0, j=s.length()-1; i<j; i++, j--)
    {
        while(i<j && !Character.isLetterOrDigit(s.charAt(i)))
            i++;
        while(i<j && !Character.isLetterOrDigit(s.charAt(j)))
            j--;
        if(i==j)
            return true;
        char left = Character.toUpperCase(s.charAt(i));
        char right = Character.toUpperCase(s.charAt(j));
        if(left != right)
            return false;
    }
    return true;
}
```

It's based on the normal palindrome question. 

Normally, you just need to compare letters from both ends to the middle.

Here are some corner cases:

1. You need to ignore non-letter and non-digital characters.
2. The palindrome is not case sensitive.
3. The input string could be empty.
4. The input string could be all non-letter and non-digital characters.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(1)`.
