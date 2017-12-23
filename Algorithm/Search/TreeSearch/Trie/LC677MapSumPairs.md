# LC677. Map Sum Pairs

### LeetCode

## Question

Implement a MapSum class with insert, and sum methods.

For the method insert, you'll be given a pair of (string, integer). The string represents the key and the integer represents the value. If the key already existed, then the original key-value pair will be overridden to the new one.

For the method sum, you'll be given a string representing the prefix, and you need to return the sum of all the pairs' value whose key starts with the prefix.

Example 1:

```
Input: insert("apple", 3), Output: Null
Input: sum("ap"), Output: 3
Input: insert("app", 2), Output: Null
Input: sum("ap"), Output: 5
```

## Solutions

* C#1
```
public class MapSum {

    private Trie root;
    
    /** Initialize your data structure here. */
    public MapSum() {
        root = new Trie();
    }
    
    public void Insert(string key, int val) {
        Trie node = root;
        foreach(char k in key){
            if(node.children[k-'a'] == null)
                node.children[k-'a'] = new Trie();
            node = node.children[k-'a'];
        }
        node.val = val;
        node.isValue = true;
    }
    
    public int Sum(string prefix) {
        Trie node = root;
        foreach(char k in prefix){
            if(node.children[k-'a'] == null)
                node.children[k-'a'] = new Trie();
            node = node.children[k-'a'];
        }
        return SumNode(node);
    }
    
    private int SumNode(Trie node){
        if(node == null) return 0;
        int res = node.isValue ? node.val : 0;
        foreach(Trie t in node.children){
            res += SumNode(t);
        }
        return res;
    }
}

class Trie{
    public Trie[] children;
    public bool isValue;
    public int val;
    
    public Trie(){
        isValue = false;
        children = new Trie[26];
    }
}

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum obj = new MapSum();
 * obj.Insert(key,val);
 * int param_2 = obj.Sum(prefix);
 */
```

## Explanation

**NOTE:** The question missed a constrains: the string is all lower case letter.

The idea is to use a Trie to store all the insert strings.

Find the node of the `prefix`, sum all values of the node's children.

* **worst-case time complexity:** O(max(keyLength))
* **worst-case space complexity:** O(n)
