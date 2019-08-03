# Lint1281. Top K Frequent Elements

### LintCode

## Question

Given a non-empty array of integers, return the k most frequent elements.

**Example 1:**
```
Input: 
nums = [1,1,1,2,2,3], k = 2

Output: 
[1,2]
```

**Example 2:**
```
Input: 
nums = [1], k = 1

Output: 
[1]
```

**Notice**
* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param nums: the given array
     * @param k: the given k
     * @return: the k most frequent elements
     */
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> count = new HashMap<>();
        for (int num : nums) {
            if (!count.containsKey(num))
                count.put(num, 0);
                
            count.put(num, count.get(num) + 1);
        }
            
        PriorityQueue<Map.Entry<Integer, Integer>> pq = new PriorityQueue(k + 1, new MyComparator());
        
        for (Map.Entry<Integer, Integer> kv : count.entrySet()) {
            pq.add(kv);
            if (pq.size() > k)
                pq.remove();
        }
        
        List<Integer> res = new ArrayList();
        for (Map.Entry<Integer, Integer> kv : pq) {
            res.add(kv.getKey());
        }
        return res;
    }
}

class MyComparator implements Comparator<Map.Entry<Integer, Integer>> { 
    public int compare(Map.Entry<Integer, Integer> a, Map.Entry<Integer, Integer> b)
    { 
        return Integer.compare(a.getValue(), b.getValue());
    } 
}
```

* Java
```
public class Solution {
    /**
     * @param nums: the given array
     * @param k: the given k
     * @return: the k most frequent elements
     */
    public List<Integer> topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> count = new HashMap<>();
        for (int num : nums) {
            if (!count.containsKey(num))
                count.put(num, 0);
                
            count.put(num, count.get(num) + 1);
        }
            
        PriorityQueue<Map.Entry<Integer, Integer>> pq = new PriorityQueue<Map.Entry<Integer, Integer>>(k + 1, 
        new Comparator<Map.Entry<Integer, Integer>>() { 
            public int compare(Map.Entry<Integer, Integer> a, Map.Entry<Integer, Integer> b)
            { 
                return Integer.compare(a.getValue(), b.getValue());
            } 
        });
        
        for (Map.Entry<Integer, Integer> kv : count.entrySet()) {
            pq.add(kv);
            if (pq.size() > k)
                pq.remove();
        }
        
        List<Integer> res = new ArrayList();
        for (Map.Entry<Integer, Integer> kv : pq) {
            res.add(kv.getKey());
        }
        return res;
    }
}
```

The idea is: first count the frequency of each element by a hashmap. Then use a priority queue to keep the k most frequent elements.

LintCode does not support Java8!!! I cannot use lambda.

**NOTE**

The question does not require the elments order in the result.

**Complexity:**

* **worst-case time complexity:** O(n * log(k)), where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `nums`.
