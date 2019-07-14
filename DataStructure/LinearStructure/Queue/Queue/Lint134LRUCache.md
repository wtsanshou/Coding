# Lint134. LRU Cache

### LintCode

## Question

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.

set(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item. Finally, you need to return the data from each get

**Example1**
```
Input:
LRUCache(2)
set(2, 1)
set(1, 1)
get(2)
set(4, 1)
get(1)
get(2)

Output: 
[1,-1,1]

Explanation：
cache cap is 2，set(2,1)，set(1, 1)，get(2) and return 1，set(4,1) and delete (1,1)，because （1,1）is the least use，get(1) and return -1，get(2) and return 1.
```

**Example 2:**
```
Input：
LRUCache(1)
set(2, 1)
get(2)
set(3, 2)
get(2)
get(3)

Output：
[1,-1,2]

Explanation：
cache cap is 1，set(2,1)，get(2) and return 1，set(3,2) and delete (2,1)，get(2) and return -1，get(3) and return 2.
```

## Solutions

### Solution 1

* Java
```
public class LRUCache {
    
    private int capacity;
    private Deque<Integer> keyQueue;
    private Map<Integer, Integer> map;
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        keyQueue = new LinkedList<>();
        map = new HashMap<>();
    }

    public int get(int key) {
        if(!map.containsKey(key))
            return -1;
        updateDeque(key);
        return map.get(key);
    }

    public void set(int key, int value) {
        if(!map.containsKey(key)){
            map.put(key, value);
            keyQueue.offer(key);
            if(keyQueue.size()>capacity){
                int removedKey = keyQueue.poll();
                map.remove(removedKey);
            }
        }
        else {
            updateDeque(key);
            map.put(key, value);
        }
    }
    
    private void updateDeque(int key){
        keyQueue.remove(key);
        keyQueue.offer(key);
    }
}
```

When I see the question, the first thing I need is a queue to keep the order of the Least Recently Used (LRU) cache. When we do `get` or `set`, we need to move the `key` to the latest place. If the queue size is bigger than the `capacity` we need to remove the oldest used `key`. So, `Deque` is perfect for these operations.

Because we also need to `get` the `value`, a `HashMap` is perfect to map these `key` in the `Deque` to their `value`s.

So the idea is to use a `Deque` and a `HashMap` to implement the Least Recently Used (LRU) cache.

**Note**

* When poll the oldest used cache from the `Deque`, do not forget to remove the `key` from the `HashMap`.
* `get` operation also need to update the `Deque`.

**get Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `keyQueue`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `keyQueue`.

**set Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `keyQueue`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `keyQueue`.
