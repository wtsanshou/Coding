# LC720. Longest Word in Dictionary

### LeetCode

## Question

Given a list of strings words representing an English Dictionary, find the longest word in words that can be built one character at a time by other words in words. If there is more than one possible answer, return the longest word with the smallest lexicographical order.

If there is no answer, return the empty string.

**Example 1:**

```
Input: 
words = ["w","wo","wor","worl", "world"]

Output: 
"world"
```

**Explanation:** 

The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".

**Example 2:**

```
Input: 
words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]

Output: 
"apple"
```

**Explanation:** 

Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".

**Note:**

* All the strings in the input will only contain lowercase letters.
* The length of words will be in the range [1, 1000].
* The length of words[i] will be in the range [1, 30].

## Solutions

* C#1
```
public class Solution {
    public string LongestWord(string[] words) {
        HashSet<string> dict = new HashSet<string>();
        foreach(string word in words)
            dict.Add(word);
        Array.Sort(words, (string a, string b) => {
            if(a.Length != b.Length) return b.Length - a.Length;
            else return a.CompareTo(b);
        });
        for(int i=0; i<words.Length; ++i)
            if(findWord(words[i], dict))
                return words[i];
        return "";
    }
    
    private bool findWord(string word, HashSet<string> dict){
        for(int i=1; i<word.Length; ++i){
            string subStr = word.Substring(0, i);
            if(!dict.Contains(subStr))
                return false;
        }
        return true;
    }
}
```

## Explanation

1. Put all words in a set
2. Check each word from the array sorted by string length and lexicographical order.
3. Check all substring of the candidate word.

Another solution might be <a href="https://en.wikipedia.org/wiki/Trie">Trie</a>

* **worst-case time complexity:** O(n*log(n))
* **worst-case space complexity:** O(n*log(n))