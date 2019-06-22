# LC524. Longest Word in Dictionary through Deleting

### LeetCode

## Question

Given a string and a string dictionary, find the longest string in the dictionary that can be formed by deleting some characters of the given string. If there are more than one possible results, return the longest word with the smallest lexicographical order. If there is no possible result, return the empty string.

**Example 1:**

```
Input:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

Output: 
"apple"
```

**Example 2:**

```
Input:
s = "abpcplea", d = ["a","b","c"]

Output: 
"a"
```

**Note:**

1.	All the strings in the input will only contain lower-case letters.
2.	The size of the dictionary won't exceed 1,000.
3.	The length of all the strings in the input won't exceed 1,000.

## Solutions

### Solution 1

* C++ (103ms)
```
string findLongestWord(string s, vector<string>& d) {
    string res;
    int maxL= 0;
    sort(d.begin(), d.end());
    reverse(d.begin(), d.end());
    for(string word : d)
    {
        int i=0;
        for(auto c : s)
        {
            if(i<word.length() && word[i]==c) i++;
        }
        if(i== word.length() && i >= maxL)
        {
            res = word;
            maxL = i;
        }
    }
    return res;
}
```

**Note** `can be formed by deleting some characters of the given string` means the order should not be changed.

1. Sort the directory by the lexicographical.
2. Reverse it, because we want to check the smallest lexicographical in final.
3. Check each word in the directory, if all the letters in the word can be found (`i== word.length()?`) in the string `s`.

**Complexity:**

* **worst-case time complexity:** `O(m * n)`, where `m` is the length of `s`, `n` is the length of word in `d`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of word in `d`.
