# Lint544. Top k Largest Numbers

## LintCode

## Question

Given an integer array, find the top k largest numbers in it.

**Example 1**
```
Input: 
[3, 10, 1000, -99, 4, 100] and k = 3

Output: 
[1000, 100, 10]
```

**Example 2**
```
Input: 
[8, 7, 6, 5, 4, 3, 2, 1] and k = 5

Output: 
[8, 7, 6, 5, 4]
```

## Solutions

### Solution 1

* Java (Time Limit Exceeded)
```
public int[] topk(int[] nums, int k) {
    int n = nums.length;
    
    for (int i = 0; i < k; i++) {
        for (int j = n - 1; j > i; j--) {
            if (nums[j] > nums[j - 1]) {
                int temp = nums[j];
                nums[j] =  nums[j - 1];
                nums[j - 1] = temp;
            } 
        }
    }
    
    return Arrays.copyOfRange(nums, 0, k);
}
```

This idea is from the bubble sort.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(1)`.


### Solution 2

* Java
```
public int[] topk(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>(k + 1);
    for (int num : nums) {
        pq.add(num);
        if (pq.size() > k)
            pq.remove();
    }
    
    int[] res = new int[k];
    
    for (int i = res.length - 1; i >= 0; i--) {
        res[i] = pq.poll();
    }
    
    return res;
    
}
```

Top K question normally use priority queue. Always keep k maximum values.

**Complexity:**

* **worst-case time complexity:** O(n * log(k)), where `n` is the length of the input `nums`.
* **worst-case space complexity:** `O(k)`.
