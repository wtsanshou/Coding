# LC345. Reverse Vowels of a String

### LeetCode

## Question

Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1:**
```
Given s = "hello", return "holle".
```

**Example 2:**

```
Given s = "leetcode", return "leotcede".
```

**Note:**

* The vowels does not include the letter "y".

## Solutions

### Solution 1

* C++ (12ms)
```
string reverseVowels(string s) {
    int vowels[128] = {0};
    vowels['a']=vowels['e']=vowels['i']=vowels['o']=vowels['u']= 1;
    vowels['A']=vowels['E']=vowels['I']=vowels['O']=vowels['U']= 1;
    int i=0, j=s.length()-1;
    while(i<j)
    {
        if(i<j && vowels[s[i]]!=1)
            i++;
        else if(i<j && vowels[s[j]]!=1)
            j--;
        else
        {
            swap(s[i], s[j]);
            i++;
            j--;
        }
    }
    return s;
}
```

* C++ (12ms)
```
string reverseVowels(string s) {
    int i=0, j= s.length()-1;
    string v = "aeiouAEIOU";
    while(i<j)
    {
        while(v.find(s[i]) == string::npos && i<j) i++;
        while(v.find(s[j]) == string::npos && i<j) j--;
        swap(s[i++], s[j--]);
    }
    return s;
}
```

* Java (6ms)
```
private boolean isVowel(char c)
{
    c = Character.toLowerCase(c);
    return (c=='a' || c=='e' || c=='i' || c=='o' || c=='u');
}
public String reverseVowels(String s) {
    char[] cs = s.toCharArray();
    int i=0, j=s.length()-1;
    while(i<j)
    {
        if(isVowel(cs[i]) && isVowel(cs[j]))
        {
            char temp = cs[i];
            cs[i++] = cs[j];
            cs[j--] = temp;
        }
        else if(isVowel(cs[i])) j--;
        else if(isVowel(cs[j])) i++;
        else {i++; j--;}
    }
    return new String(cs);
}
```

Find vowel from both side, and then swap them. Continue until the whole string.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(1)`.