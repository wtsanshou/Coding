# LC211. Add and Search Word

### LeetCode

## Question

Design a data structure that supports the following two operations:

```
void addWord(word)
bool search(word)
search(word) can search a literal word or a regular expression string containing only letters a-z or `.` means it can represent any one letter.
```

**For example:**
```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

**Note:**

You may assume that all words are consist of lowercase letters a-z.

You should be familiar with how a Trie works. If not, please work on this problem: Implement Trie (Prefix Tree) first.

## Solutions

### Solution 1

* C++
```
/**
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * bool param_2 = obj.search(word);
 */

class Trie{
public:
    vector<Trie*> children;
    bool isWord;
    Trie()
    {
        children = vector<Trie*>(26);
        isWord=false;
    }
};

class WordDictionary {
private:
    Trie* root;
public:
    /** Initialize your data structure here. */
    WordDictionary() {
        root = new Trie();
    }
    
    bool checkAllChriden(string& word, Trie* root, int star)
    {
        for(auto child : root->children)
            if(child!=NULL)
                if(searchWordFromTrie(word, child, star)) return true;
        return false;
    }
    bool searchWordFromTrie(string& word, Trie* root, int start)
    {
        if(start==word.length()) return root->isWord;
        for(int i=start; i<word.length(); ++i)
        {
            if(word[i]=='.') return checkAllChriden(word, root, i+1);
            else if(root->children[word[i]-'a'] == NULL) return false;
            else return searchWordFromTrie(word, root->children[word[i]-'a'], i+1);
        }
        return false;
    }
    
    /** Adds a word into the data structure. */
    void addWord(string word) {
        Trie* cur = root;
        for(char w : word)
        {
            if(cur->children[w-'a'] == NULL)
                cur->children[w-'a'] = new Trie();
            cur = cur->children[w-'a'];
        }
        cur->isWord = true;
    }
    
    /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
    bool search(string word) {
        return searchWordFromTrie(word, root, 0);
    }
};
```

* C++
```
class WordDictionary {
public:
    struct Trie{
      vector<Trie*> child;
      bool isWord;
      Trie(): isWord(false), child(vector<Trie*>(26, nullptr)){}
    };

    Trie* root;
    WordDictionary()
    {
        root = new Trie();
    }

    // Adds a word into the data structure.
    void addWord(string word) {
        int len = word.size();
        Trie* cur = root;
        for(int i=0; i<len; ++i)
        {
            int index = word[i]-'a';
            if(cur->child[index]==NULL) cur->child[index] = new Trie();
            cur = cur->child[index];
        }
        cur->isWord = true;
    }

    bool search(const char * c, Trie* cur)
    {
        if(cur==NULL) return false;
        if(*c == '\0') return cur->isWord;
        if(*c == '.') 
        {
            for(int i=0; i<26; ++i) 
            {
                if(search(c+1, cur->child[i])) return true;
            }
            return false;
        }
        else
            return search(c+1, cur->child[*c-'a']);
        
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    bool search(string word) {
        return search(word.c_str(), root);
    }
};
```

**addWord Complexity:**

* **worst-case time complexity:** `O(w)`, where `w` is the length of the input `word`.
* **worst-case space complexity:** `O(26w)`, where `w` is the length of the input `word`.

**search Complexity:**

* **worst-case time complexity:** `O(26w)`, where `w` is the length of the input `word`.
* **worst-case space complexity:** `O(1)`.
