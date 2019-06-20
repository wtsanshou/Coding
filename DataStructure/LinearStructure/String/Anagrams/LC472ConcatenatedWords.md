# LC472. Concatenated Words

### LeetCode

## Question

Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.

A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.

**Example:**

```
Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]

Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]

Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
 "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
"ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".
```

**Note:**

1.	The number of elements of the given array will not exceed 10,000
2.	The length sum of elements in the given array will not exceed 600,000.
3.	All the input string will only include lower case letters.
4.	The returned elements order does not matter.

## Solutions

### Solution 1

* C++ (MLE)
```
class Solution {
public:
    bool isConcatenatedWord(unordered_map<string, bool>& map, string& word)
    {
        if(map[word]==true) return true;
        for(int i=1; i<word.length(); ++i)
        {
            string left = word.substr(0, i);
            string right = word.substr(i);
            if(map[left] == true && isConcatenatedWord(map, right))
            {
                //map[word] = true;
                return true;
            }
        }
        return false;
    }
    vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
        unordered_map<string, bool> map;
        vector<string> res;
        sort(words.begin(), words.end(), [](string a, string b) {return a.length()<b.length();});
        map[""] = true;
        for(string word : words)
        {
            if(isConcatenatedWord(map, word))
                res.push_back(word);
            map[word] = true;
        }
        return res;
    }
};
```

* C++ (TLE)
```
vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
    unordered_map<string, bool> map;
    vector<string> res;
    sort(words.begin(), words.end(), [](string a, string b) {return a.length()<b.length();});
    int min = words[0].size();
    for(string word : words)
    {
        string temp = word;
        for(int i=min; i<temp.length(); ++i)
        {
            string left = word.substr(0, i);
            if(map[left] == true)
            {
                string right = word.substr(i);
                if(map[right]==true) res.push_back(word);
                temp=right;
                i=min;
            }
        }
        map[word] = true;
    }
    return res;
}
```

1. Sort the words by their size.
2. Check each word, cut it to left and right substrings
3. If left and right substrings are both in the map, put it into the result.

**Complexity:**

* **worst-case time complexity:** O(m * n<sup>2</sup>), where `m` is the number of `words`, `n` is the length of `word`.
* **worst-case space complexity:** `O(m)`, where `m` is the number of `words.

### Solution 2

* C++ (TLE)
```
class Solution {
public:
    bool isConcatenatedWord(unordered_map<string, bool>& map, string& word)
    {
        if(word.empty()) return true;
        vector<bool> dp(word.length()+1);
        dp[0] = true;
        for(int i=1; i<=word.length(); ++i)
        {
            for(int j=0;j<i; ++j)
            {
                if(dp[j]==true && map[word.substr(j, i-j)]==true) //left is concatenate, right is in map
                {
                    dp[i] = true;
                    break;
                }    
            }
        }
        return dp[word.length()];
    }
    vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
        unordered_map<string, bool> map;
        vector<string> res;
        sort(words.begin(), words.end(), [](string a, string b) {return a.length()<b.length();});
        for(string word : words)
        {
            if(isConcatenatedWord(map, word))
                res.push_back(word);
            map[word] = true;
        }
        return res;
    }
};
```

* C++ (662ms)
```
vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
    unordered_map<string, bool> map;
    vector<string> res;
    sort(words.begin(), words.end(), [](string a, string b) {return a.length()<b.length();});
    for(string word : words)
    {
        int n=word.length();
        if(n==0) continue;
        vector<int> mem(n+1);
        mem[0] = 1;
        for(int i=1; i<=n; ++i)
        {
            for(int j=0;j<i; ++j)
            {
                if(mem[j]==1 && map[word.substr(j, i-j)]==true) //left is concatenate, right is in map
                {
                    mem[i] = 1;
                    break;
                }    
            }
        } 
        if(mem[n]==1) res.push_back(word);
        map[word] = true;
    }
    return res;
}
```

For each word, use `mem[i]` to remember if the `word.substr(0,j)` is in the map. So we don't need to recalculate it again.

**Complexity:**

* **worst-case time complexity:** O(m * n<sup>2</sup>), where `m` is the number of `words`, `n` is the length of `word`.
* **worst-case space complexity:** `O(max(m,n))`, where `m` is the number of `words`, `n` is the length of `word`.

### Solution 3
* C++ (MLE)
```
class Trie{
public:
    vector<Trie*> child;
    bool isWord;
    Trie(){
        child = vector<Trie*>(26);
        isWord=false; //strange, default should be false, but it seems not
    }
};

class Solution {
public:
    void addWord(string& word, Trie* root)
    {
        Trie* cur = root;
        for(char w : word)
        {
            if(cur->child[w-'a']==NULL)
                cur->child[w-'a'] = new Trie();
            cur = cur->child[w-'a'];
        }
        cur->isWord = true;
    }
    bool isConcatenateWord(string& word, int start, Trie* root, int wordCount)
    {
        Trie* cur = root;
        int n = word.length();
        for(int i=start; i<n; ++i)
        {
            if(cur->child[word[i]-'a']==NULL) return false;
            
            if(cur->child[word[i]-'a']->isWord == true)
            {
                if(i==n-1) return wordCount>=1;
                if(isConcatenateWord(word, i+1, root, wordCount+1))
                    return true;
            }
            cur = cur->child[word[i]-'a'];
        }
        return false;
    }
    vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
        Trie* root = new Trie();
        vector<string> res;
        for(int i=0; i<words.size(); ++i)
        {
            if(!words[i].empty())
                addWord(words[i], root);
        }
        for(int i=0; i<words.size(); ++i)
        {
            if(!words[i].empty() && isConcatenateWord(words[i], 0, root, 0))
                res.push_back(words[i]);
        }
        return res;
    }
};
```

Tried to use trie instead of map. But it will consume too much memory.

**Complexity:**

* **worst-case time complexity:** O(m * n<sup>2</sup>), where `m` is the number of `words`, `n` is the length of `word`.
* **worst-case space complexity:** `O(m*n)`, where `m` is the number of `words`, `n` is the length of `word`.

