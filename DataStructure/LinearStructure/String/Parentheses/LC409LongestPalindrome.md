# LC409. Longest Palindrome

### LeetCode

## Question

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

**Note:**

Assume the length of given string will not exceed 1,010.

**Example:**

```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

## Solutions

### Solution 1

* Java (6ms)
```
int longestPalindrome(string s) {
    int res = 0;
    int count[128] = {0};
    for(char c : s)
        count[c]++;
    int hasOdd = 0;
    for(int i='A'; i<='z'; ++i)
    {
        if(count[i]%2==0) res += count[i];
        else 
        {
            res += count[i]-1;
            hasOdd = 1;
        }
    }
    return res + hasOdd;
}
```

To build a palindrome, you will find there are only two cases:

1. The number of all elements are even.
2. Only one element could be odd.

So the solution is very clear now. You just need to count the number of each letter in the `s`. Add all possible even number of elements into result. Finally, add `1` into result if odd number of element exists in the `s`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.  
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`

### Solution 2

* C++ (3ms)
```
int longestPalindrome(string s) {
    int letter[128] = {0}, n = s.length();
    for(int i=0; i<n; ++i)
        letter[s[i]]++;
    int res = 0, odd = 0;
    for(int i=65; i<=122; ++i)
    {
        res += letter[i];
        if(letter[i]%2 != 0)
            odd++;
    }
    return (odd>1) ? res-odd+1 : res;
}
```

* Java (1ms)
```
public int longestPalindrome(String s) {
    char[] sc = s.toCharArray();
    
    int[] count = new int[128];
    for(char c : sc)
        count[c]++;
    
    int oddN = 0;
    for(int i=65; i<=122; i++)
        if(count[i]%2 != 0) oddN++;
    
    return oddN>0 ? sc.length-oddN+1 : sc.length;
}
```

We want even number of each elements to build a palindrome. We know `odd-1 = even`. So we can just count the number of odd elements in the `count`. We just need to minus it from the total length of the `s`. Becase at most one odd element is accepted, we can add `1` back if odd element exists in the `count`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.  
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`

