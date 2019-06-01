# LC567. Permutation in String

### LeetCode

## Question

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

**Example 1:**
```
Input:s1 = "ab" s2 = "eidbaooo"
Output:True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**
```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

**Note:**

1.	The input strings only contain lower case letters.
2.	The length of both given strings is in range [1, 10,000].

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    bool hasSameLetters(string& sub, vector<int>& ls)
    {
        vector<int> ls2(26,0);
        for(char c : sub)
            ls2[c-'a']++;
        for(int i=0; i<26; ++i)
            if(ls[i] != ls2[i]) return false;
        return true;
    }
    bool checkInclusion(string s1, string s2) {
        vector<int> ls(26,0);
        for(char c : s1)
            ls[c-'a']++;
        int subS= s1.length();
        for(int i=0; i+subS<=s2.size(); ++i)
        {
            string sub = s2.substr(i, subS);
            if(hasSameLetters(sub, ls)) return true;
        }
        return false;
    }
};
```

Check all length of `s1` substring in `s2`. Check if they are anagrams.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `s1`, `m` is the maximum legth of the string in the `s2`.
* **worst-case space complexity:** `O(1)`.