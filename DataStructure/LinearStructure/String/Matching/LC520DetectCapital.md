# LC520. Detect Capital

### LeetCode

## Question

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:

1.	All letters in this word are capitals, like "USA".
2.	All letters in this word are not capitals, like "leetcode".
3.	Only the first letter in this word is capital if it has more than one letter, like "Google".

Otherwise, we define that this word doesn't use capitals in a right way.

**Example 1:**

```
Input: "USA"
Output: True
```

**Example 2:**
```
Input: "FlaG"
Output: False
```

**Note:** 

* The input will be a non-empty word consisting of uppercase and lowercase latin letters.

## Solutions

### Solution 1

* C++ (18ms)
```
bool detectCapitalUse(string word) {
    char first = word[0];
    if(isupper(first))
    {
        for(int i=2; i<word.size(); ++i)
            if(isupper(word[i]) ^ isupper(word[i-1])) return false;
    }
    else
        for(int i=1; i<word.size(); ++i)
            if(isupper(word[i])) return false;
    return true;
}
```

* Python
```
def detectCapitalUse(self, word):
    if len(word)==1 :
        return True
    if word[0].isupper():
        return word[1:].isupper() or word[1:].islower()
    else:
        return word[1:].islower()
```

* Python
```
def detectCapitalUse(self, word):
    return word.isupper() or word.islower() or word.istitle()
```

1. Capital start:
1.1. All uppercase following return true, otherwise, return false
1.2. All lowercase following return true, otherwise, return false

2. Lowercase start, all lowercase following return true, otherwise, return false

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `words`.
* **worst-case space complexity:** `O(1)`.


## Test cases:
```
Id	Testcase	Result
1	A	        True
2	a	        True
3	AB	        True
4	ab	        True
5	Ab	        True
6	aB	        False
7	AbA	        False
8	aBa	        False
9	aBA	        False
10	Aba	        True
11	abA	        False
	NULL	
	Other characters than alphbetic	
```		

