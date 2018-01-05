# LC676. Implement Magic Dictionary

### LeetCode

## Question

Implement a magic directory with buildDict, and search methods.

For the method buildDict, you'll be given a list of non-repetitive words to build a dictionary.

For the method search, you'll be given a word, and judge whether if you modify exactly one character into another character in this word, the modified word is in the dictionary you just built.

**Example 1:**

```
Input: buildDict(["hello", "leetcode"]), Output: Null
Input: search("hello"), Output: False
Input: search("hhllo"), Output: True
Input: search("hell"), Output: False
Input: search("leetcoded"), Output: False
```

**Note:**

You may assume that all the inputs are consist of lowercase letters a-z.
For contest purpose, the test data is rather small by now. You could think about highly efficient algorithm after the contest.

Please remember to RESET your class variables declared in class MagicDictionary, as static/class variables are persisted across multiple test cases. Please see here for more details.

## Solutions

```
/**
 * Your MagicDictionary object will be instantiated and called as such:
 * MagicDictionary obj = new MagicDictionary();
 * obj.BuildDict(dict);
 * bool param_2 = obj.Search(word);
 */
```

* C#1
```
public class MagicDictionary {

    private HashSet<string> myDict;
    
    /** Initialize your data structure here. */
    public MagicDictionary() {
        myDict = new HashSet<string>();
    }
    
    /** Build a dictionary through a list of words */
    public void BuildDict(string[] dict) {
        foreach(string word in dict)
            myDict.Add(word);
    }
    
    /** Returns if there is any word in the trie that equals to the given word after modifying exactly one character */
    public bool Search(string word) {
        for(int i=0; i<word.Length; ++i){
            for(char m='a'; m<word[i]; ++m)
                if(ContainsModifiedWord(word, i, m)) return true;
            for(char n='z'; n>word[i]; --n)
                if(ContainsModifiedWord(word, i, n)) return true;
        }
        return false;
    }
    
    private bool ContainsModifiedWord(string word, int i, char x){
        char[] temp = word.ToCharArray();
        temp[i] = x;
        return myDict.Contains(new string(temp));
    }
}
```

## Explanation

* **worst-case space complexity:** O(n)

**BuildDict**

Put all dict words into a set.

* **worst-case time complexity:** O(n)

**Search**

The idea is to change each letter to other letter, and see if the modifed word is in the set.

* **worst-case time complexity:** O(Len(word))


