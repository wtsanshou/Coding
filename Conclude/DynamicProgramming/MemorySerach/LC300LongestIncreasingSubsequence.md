# LC300. Longest Increasing Subsequence

### LeetCode

## Question

Given an unsorted array of integers, find the length of longest increasing subsequence.

**For example**
```
Given [10, 9, 2, 5, 3, 7, 101, 18],
The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.
```

Your algorithm should run in `O(n2)` complexity.

**Follow up:** Could you improve it to `O(n*log(n))` time complexity?

## Solutions

### Solution 1

* C++ (6ms) set
```
int lengthOfLIS(vector<int>& nums) {
    set<int> lis;
    for(auto num : nums)
    {
        if(lis.find(num) == lis.end())
        {
            lis.insert(num);
            auto it = lis.upper_bound(num);
            if(it != lis.end())
                lis.erase(it);
        }
    }
    return lis.size();
}
```

* Java1 (1ms) using Array as stack
```
public int lengthOfLIS(int[] nums) {
    int len = nums.length;
    int[] stack = new int[len];
    int top =-1;
    for(int num : nums)
    {
        int cur = top;
        while(cur!=-1 && stack[cur]>=num)
            cur--;
        if(cur == top)
            top++;
        stack[++cur] = num; //replace upper bound
    }
    return top + 1;
}
```

* Java2
```
public int lengthOfLIS(int[] nums) {
    int len = nums.length;
    int[]  LIS = new int[len];
    int size = 0;
    for(int num : nums)
    {
        int i = Arrays.binarySearch( LIS, 0, size, num);
        if(i<0) i = -(i+1);
         LIS[i] = num;
        if(i==size) size++;
    }
    return size;
}
```

* Java3 
```
public int lengthOfLIS(int[] nums) {
    LinkedList<Integer>  LIS = new LinkedList<Integer>();
    for(int num : nums)
    {
        if( LIS.isEmpty() ||  LIS.getLast() < num)
             LIS.add(num);
        else
        {
            int i = Collections.binarySearch( LIS, num);
             LIS.set((i<0)? -(i+1) : i, num);
        }
    }
    return  LIS.size();
}
```

Using a container to hold the Longest Increasing Subsequence `LIS`. For a comming number:

1. If the number `num` is larger than all numbers in the `LIS`, add the number in the `LIS`. (only this can increase the length of the `LIS`)
2. else, replace the upper bound number of the `num` in the `LIS`. (it will not affect the length of the `LIS`, but it gives chances for smaller number to increase the length of the `LIS`).

Using TreeSet could be faster.

**Complexity:**

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.

### Solution 2

* Java (Time Limit Exceeded)
```
public class Solution {
    /**
     * @param nums: An integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        int max = 0;
        for (int i = 0; i < nums.length; i++) {
            max = Math.max(max, dfs(nums, i, nums[i], 1));
        }
        return max;
    }
    
    private int dfs(int[] nums, int start, int lastNum, int len) {
        if (start >= nums.length) {
            return len;
        }
        
        int max = len;
        
        for (int i = start + 1; i < nums.length; i++)
            if (nums[i] > lastNum)
                max = Math.max(max, dfs(nums, i, nums[i], len + 1));
        
        return max;
    }
}
```

Almost all finding combination in a group of values can use `DFS` solution to search all possible combinations. But this method is too slow, because it may have a lot of duplicate calculation. With duplicate calculation, we can think of `DP`. 

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.

### Solution 3

* Java
```
public class Solution {
    /**
     * @param nums: An integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        int max = 0;
        int[] mem = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            max = Math.max(max, dfs(nums, i, nums[i], 1, mem));
        }
        return max;
    }
    
    private int dfs(int[] nums, int start, int lastNum, int len, int[] mem) {
        if (start >= nums.length) {
            return len;
        }
        if (mem[start] != 0) return mem[start];
        int max = len;
        
        for (int i = start + 1; i < nums.length; i++)
            if (nums[i] > lastNum)
                max = Math.max(max, len + dfs(nums, i, nums[i], 1, mem));
        
        mem[start] = max;
        return max;
    }
}
```

From **Solution 2**, `max = Math.max(max, dfs(nums, i, nums[i], len + 1));` will be invoked many time starting from each element. To avoid the duplicated calculation, we can use a memory to remember the length of longest increasing subsequence starting from `i`.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.



