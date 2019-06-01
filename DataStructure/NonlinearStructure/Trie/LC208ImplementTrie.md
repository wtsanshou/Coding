# LC208. Implement Trie

### LeetCode

## Question

Implement a trie with insert, search, and startsWith methods.

**Note:**

You may assume that all inputs are consist of lowercase letters a-z.

## Solution

### Solution 1

* C++
```
class TrieNode{
public:
    vector<TrieNode*> node;
    bool isWord;
    TrieNode(){
        isWord = false;
        node = vector<TrieNode*>(26, nullptr);
    }
};

class Trie {
private:
    TrieNode* root;
    TrieNode* find(string& word)
    {
        TrieNode* cur = root;
        for(int i=0; i<word.length() && cur!=NULL; ++i)
        {
            cur = cur->node[word[i]-'a'];
        }
        return cur;
    }
public:
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* cur = root;
        for(char w : word)
        {
            if(cur->node[w-'a'] == NULL) cur->node[w-'a'] = new TrieNode();
            cur=cur->node[w-'a'];
        }
        cur->isWord = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* res = find(word);
        return res!=NULL && res->isWord;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        return find(prefix)!=NULL;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * bool param_2 = obj.search(word);
 * bool param_3 = obj.startsWith(prefix);
 */
```

**insert Complexity:**

* **worst-case time complexity:** `O(w)`, where `w` is the length of the input `word`.
* **worst-case space complexity:** `O(26w)`, where `w` is the length of the input `word`.

**search Complexity:**

* **worst-case time complexity:** `O(w)`, where `w` is the length of the input `word`.
* **worst-case space complexity:** `O(1)`.

**startsWith Complexity:**

* **worst-case time complexity:** `O(p)`, where `p` is the length of the input `prefix`.
* **worst-case space complexity:** `O(1)`.