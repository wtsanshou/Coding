# LC953. Verifying an Alien Dictionary

### LeetCode

## Question

In an alien language, surprisingly they also use english lowercase letters, but possibly in a different order. The order of the alphabet is some permutation of lowercase letters.

Given a sequence of words written in the alien language, and the order of the alphabet, return true if and only if the given words are sorted lexicographicaly in this alien language.

**Example 1:**
```
Input: words = ["hello","leetcode"], order = "hlabcdefgijkmnopqrstuvwxyz"
Output: true
Explanation: As 'h' comes before 'l' in this language, then the sequence is sorted.
```

**Example 2:**
```
Input: words = ["word","world","row"], order = "worldabcefghijkmnpqstuvxyz"
Output: false
Explanation: As 'd' comes after 'l' in this language, then words[0] > words[1], hence the sequence is unsorted.
```

**Example 3:**
```
Input: words = ["apple","app"], order = "abcdefghijklmnopqrstuvwxyz"
Output: false
Explanation: The first three characters "app" match, and the second string is shorter (in size.) According to lexicographical rules "apple" > "app", because `l` > `∅`, where `∅` is defined as the blank character which is less than any other character (More info).
```

**Note:**

* 1 <= words.length <= 100
* 1 <= words[i].length <= 20
* order.length == 26
* All characters in words[i] and order are english lowercase letters.

## Solutions

* Java1
```
class Solution {
    public boolean isAlienSorted(String[] words, String order) {
        Map<Character, Integer> dict = new HashMap<>();
        for(int i=0; i < order.length(); ++i)
            dict.put(order.charAt(i), i);
        for(int i=0; i < words.length-1; ++i){
            if(isNotOrdered(words[i], words[i+1], dict)) return false;
        }
        return true;
    }
    
    private boolean isNotOrdered(String w1, String w2, Map<Character, Integer> dict){
        for(int i=0; i < w1.length() && i < w2.length(); ++i){
            if(dict.get(w1.charAt(i)) < dict.get(w2.charAt(i))) return false;
            if(dict.get(w1.charAt(i)) > dict.get(w2.charAt(i))) return true;
        }
        return w1.length() > w2.length();
    }
}
```

## Explanation

The order is based on the most front character in the word no need to compare all the characters in the word.

* **worst-case time complexity:** O(N*M), where `N` is the number of the words, `M` is the length of the word.
* **worst-case space complexity:** O(1)
