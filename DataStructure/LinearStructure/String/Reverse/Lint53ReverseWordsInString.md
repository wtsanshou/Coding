# Lint53. Reverse Words in a String

### LintCode

## Question

Given an input string, reverse the string word by word.


**Example 1:**

```
	Input:  "the sky is blue"
	Output:  "blue is sky the"
	
	Explanation: 
	return a reverse the string word by word.
```

**Example 2:**
```
	Input:  "hello world"
	Output:  "world hello"
	
	Explanation: 
	return a reverse the string word by word.
```

**Clarification**
* What constitutes a word?

A sequence of non-space characters constitutes a word and some words have punctuation at the end.

* Could the input string contain leading or trailing spaces?

Yes. However, your reversed string should not contain leading or trailing spaces.

* How about multiple spaces between two words?

Reduce them to a single space in the reversed string.

## Solutions

### Solution 1

* Java
```
public String reverseWords(String s) {
    String input = s.trim();
    String[] words = input.split("\\s+");
    
    for(int i=0, j=words.length-1; i<j; i++, j--){
        String temp = words[i];
        words[i] = words[j];
        words[j] = temp;
    }

    return String.join(" ", words);
}
```

The key of this question is to clean the leading, trailing, and multiple spaces in the input string.

1. Using `trim()` to solve the leading or trailing spaces.
2. Using `split("\\s+")` regex to solve the multiple spaces between two words.
3. Using `String.join(" ", words)` to convert String array to a String.

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `s`.
