# LC438. Find All Anagrams in a String

### LeetCode

## Question

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## Solutions

### Solution 1

* C++ (1375 ms)
```
class Solution {
public:
    bool isAnagrams(string x, string y)
    {
        int count[128] = {0};
        for(int i=0; i<x.length(); ++i)
        {
            ++count[x[i]];
            --count[y[i]];
        }
        for(int i=0; i<x.length(); ++i)
        {
            if(count[x[i]]!=0) return false;
        }
        return true;
    }
    vector<int> findAnagrams(string s, string p) {
        vector<int> res;
        int sLen=s.length(), pLen=p.length();
        if(sLen<pLen) return res;
        for(int i=0; i<=sLen-pLen; ++i)
        {
            if(isAnagrams(s.substr(i, pLen), p))
            {
                res.push_back(i);
            }
        }
        return res;
    }
};
```

Check each substring to see if it is anagram of `p`.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `s`, `m` is the length of the input `p`.
* **worst-case space complexity:** `O(m)`, where `m` is the length of the input `p`.

### Solution 2

* C++ (56 ms)
```
vector<int> findAnagrams(string s, string p) {
    vector<int> res;
    if(s.length()==0) return res;
    int left=0, right=0, pLen = p.length(), count = pLen;
    int letters[128] = {0};
    for(char c : p) letters[c]++;
    while(right < s.length())
    {
        if(letters[s[right]]-- > 0)
            count--;
        right++;
        
        if(count==0) res.push_back(left);
        
        if(right-left == pLen)
        {
            if(letters[s[left]]++ >= 0)
                count++;
            left++;
        }
    }
    return res;
}
```

1. Add letters of `p` into the map `letters`.
2. Keep a window length of `pLen`. Move the letters of the window into the map `letters` (`letters[s[right]]--`). And count the letter is in `p` as well (the count of the letter is more than `0`).
3. `count==0` means find a matched anagrams.
4. Move the most left letter of the window out of the map (`letters[s[left]]++`). `letters[s[left]] >=0` means the letter is in `p`, it should be negative if it's not in `p`. Because in previous step, we mius it from the map `letters`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(128)`.

### Solution 3

* Java
```
public List<Integer> findAnagrams(String s, String p){
    List<Integer> res = new ArrayList<>();
    if(s.length() < p.length()) return res;
    int[] pLetters = new int[26];
    int[] sLetters = new int[26];
    char[] sc = s.toCharArray();
    char[] pc = p.toCharArray();
    for(char c : pc)
        pLetters[c-'a']++;

    for(int i=0, j=0; j<sc.length; ){
        while(j-i<pc.length && j<sc.length) sLetters[sc[j++]-'a']++;
        if(isTheSame(pLetters, sLetters)) res.add(i);
        sLetters[sc[i++]-'a']--;
    }

    return res;
}

private bool isTheSame(int[] pLetters, int[] sLetters){
    for(int i=0; i<26; i++)
        if(pLetters[i] != sLetters[i]) return false;
    return true;
}
```

Each time count the letter of the window size `pc.length`. Compare the two maps `pLetters` and `sLetters`.

Remove the most left letter of the window from the map `sLetters` and add the right letter of the window to the map `sLetters`, and compare again.

**Complexity:**

* **worst-case time complexity:** `O(26 * n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(26)`.
