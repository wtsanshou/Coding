# Lint545. Top k Largest Numbers II

### LintCode

## Question

Implement a data structure, provide two interfaces:

add(number). Add a new number in the data structure.

topk(). Return the top k largest numbers in this data structure. k is given when we create the data structure.

**Example 1**
```
Input: 
s = new Solution(3);
s.add(3)
s.add(10)
s.topk()
s.add(1000)
s.add(-99)
s.topk()
s.add(4)
s.topk()
s.add(100)
s.topk()
		
Output: 
[10, 3]
[1000, 10, 3]
[1000, 10, 4]
[1000, 100, 10]

Explanation:
s = new Solution(3);
>> create a new data structure, and k = 3.
s.add(3)
s.add(10)
s.topk()
>> return [10, 3]
s.add(1000)
s.add(-99)
s.topk()
>> return [1000, 10, 3]
s.add(4)
s.topk()
>> return [1000, 10, 4]
s.add(100)
s.topk()
>> return [1000, 100, 10]
```

**Example 2**
```
Input: 
s = new Solution(1);
s.add(3)
s.add(10)
s.topk()
s.topk()

Output: 
[10]
[10]

Explanation:
s = new Solution(1);
>> create a new data structure, and k = 1.
s.add(3)
s.add(10)
s.topk()
>> return [10]
s.topk()
>> return [10]
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    
    private PriorityQueue<Integer> pq;
    private int k;

    public Solution(int k) {
        pq = new PriorityQueue<>(k + 1);
        this.k = k;
    }

    public void add(int num) {
        pq.add(num);
        if (pq.size() > k)
            pq.remove();
    }

    public List<Integer> topk() {
        List<Integer> kElements = new ArrayList<>();
        for (Integer ele : pq)
            kElements.add(ele);
        Collections.sort(kElements, (a, b) -> Integer.compare(b, a));
        return kElements;
    }
}
```

To keep top k elements, we can use a minimum heap to remove the minimum element in the heap.

**NOTE** the question needs sorted list.

**add() Complexity:**

* **worst-case time complexity:** `O(log(k))`.
* **worst-case space complexity:** `O(k)`.

**topk() Complexity:**

* **worst-case time complexity:** `O(k * log(k))`.
* **worst-case space complexity:** `O(k)`.