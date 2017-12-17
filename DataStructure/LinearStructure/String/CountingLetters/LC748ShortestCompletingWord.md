# LC748. Shortest Completing Word

### LeetCode

## Question

Find the minimum length word from a given dictionary `words`, which has all the letters from the string `licensePlate`. Such a word is said to complete the given string `licensePlate`

Here, for letters we ignore case. For example, `"P"` on the `licensePlate` still matches "p" on the word.

It is guaranteed an answer exists. If there are multiple answers, return the one that occurs first in the array.

The license plate might have the same letter occurring multiple times. For example, given a `licensePlate` of `"PP"`, the word `"pair"` does not complete the `licensePlate`, but the word `"supper"` does.

**Example 1:**

**Input:** 

```
licensePlate = "1s3 PSt", words = ["step", "steps", "stripe", "stepple"]
```

**Output:**

```
"steps"
```

**Explanation:**

The smallest length word that contains the letters "S", "P", "S", and "T".
Note that the answer is not "step", because the letter "s" must occur in the word twice.

Also note that we ignored case for the purposes of comparing whether a letter exists in the word.

**Example 2:**

**Input:** 

```
licensePlate = "1s3 456", words = ["looks", "pest", "stew", "show"]
```

**Output:** 

```
"pest"
```

**Explanation:** 

There are 3 smallest length words that contains the letters "s".
We return the one that occurred first.

**Note:**

* licensePlate will be a string with length in range [1, 7].
* licensePlate will contain digits, spaces, or letters (uppercase or lowercase).
* words will have a length in the range [10, 1000].
* Every words[i] will consist of lowercase letters, and have length in range [1, 15].

## Solutions

* C#1
```
public class Solution {
    public string ShortestCompletingWord(string licensePlate, string[] words) {
        Dictionary<char, int> dict = GetDictionary(licensePlate);
        int maxLen = 16, res = 0;
        for(int i=0; i<words.Length; ++i){
            char[] count = new char[26];
            foreach(char c in words[i])
                count[c-'a']++;
            bool contains = true;
            foreach(char k in dict.Keys){
                if(dict[k] > count[k-'a']){
                    contains = false;
                    break;
                }
            }
            if(contains && words[i].Length < maxLen){
                maxLen = words[i].Length;
                res = i;
            }
        }
        return words[res];
    }
    
    private Dictionary<char, int> GetDictionary(string licensePlate){
        Dictionary<char, int> dict = new Dictionary<char, int>();
        foreach(char c in licensePlate){
            if(Char.IsLetter(c)){
                char x = Char.ToLower(c);
                if(dict.ContainsKey(x))
                    dict[x]++;
                else 
                    dict.Add(x, 1);
            }
        }
        return dict;
    }
}
```

## Explanation

1. Count the number of each letter in `licensePlate`
2. Count the number of each letter in each word.
3. Check if the word complete the `licensePlate`

**Corner case:** Both the word and the `licensePlate` contain the same letter, but the word contains more number of the letter than the `licensePlate`.

* **worst-case time complexity:** O(d + n*(w+d)), where `d` is the length of the `licensePlate`, `n` is the length of the words array, `w` is the maximum word length of the words.
* **worst-case space complexity:** O(d + 26)