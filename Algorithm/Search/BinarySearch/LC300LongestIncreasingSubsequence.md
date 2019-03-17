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

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the length of the `nums`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the `nums`.


