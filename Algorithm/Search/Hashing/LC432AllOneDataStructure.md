# LC432. All O`one Data Structure

### LeetCode

## Question

Implement a data structure supporting the following operations:

1.	Inc(Key) - Inserts a new key with value 1. Or increments an existing key by 1. Key is guaranteed to be a non-empty string.
2.	Dec(Key) - If Key's value is 1, remove it from the data structure. Otherwise decrements an existing key by 1. If the key does not exist, this function does nothing. Key is guaranteed to be a non-empty string.
3.	GetMaxKey() - Returns one of the keys with maximal value. If no element exists, return an empty string "".
4.	GetMinKey() - Returns one of the keys with minimal value. If no element exists, return an empty string "".


**Challenge:** Perform all these in O(1) time complexity. (If I am right, this is not possible!)

## Solutions

### Solution 1

* C++
```
class AllOne {
public:
    unordered_map<string, int> keyToVal;
    map<int, unordered_set<string>> valToKey;
    /** Initialize your data structure here. */
    AllOne() {
        keyToVal.clear();
        valToKey.clear();
    }
    void removeValKey(int val, string key)
    {
        valToKey[val].erase(key);
        if(valToKey[val].empty()) valToKey.erase(val);
    }
    /** Inserts a new key <Key> with value 1. Or increments an existing key by 1. */
    void inc(string key) {
        keyToVal[key]++;
        valToKey[keyToVal[key]].insert(key); //O(log(n)), valToKey is ordered map
        if(keyToVal[key]==1) return;
        removeValKey(keyToVal[key]-1, key);
    }
    
    /** Decrements an existing key by 1. If Key's value is 1, remove it from the data structure. */
    void dec(string key) {
        if(keyToVal.count(key)==0) return;
        removeValKey(keyToVal[key], key);
        keyToVal[key]--;
        
        if(keyToVal[key]==0)
        {
            keyToVal.erase(key);
            return;
        }
        valToKey[keyToVal[key]].insert(key);
    }
    
    /** Returns one of the keys with maximal value. */
    string getMaxKey() {
        if(valToKey.empty()) return "";
        return *(valToKey.rbegin()->second.begin());
    }
    
    /** Returns one of the keys with Minimal value. */
    string getMinKey() {
        if(valToKey.empty()) return "";
        return *(valToKey.begin()->second.begin());
    }
};

/**
 * Your AllOne object will be instantiated and called as such:
 * AllOne obj = new AllOne();
 * obj.inc(key);
 * obj.dec(key);
 * string param_3 = obj.getMaxKey();
 * string param_4 = obj.getMinKey();
 */
```

Using one map to map key to value, another map to map value to keys.

**removeValKey Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.

**inc Complexity:**

* **worst-case time complexity:** `O(log(n))` where `n` is the keys in the map valToKey.
* **worst-case space complexity:** `O(1)`.

**dec Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.

**getMaxKey Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.

**getMinKey Complexity:**

* **worst-case time complexity:** `O(1)`.
* **worst-case space complexity:** `O(1)`.
